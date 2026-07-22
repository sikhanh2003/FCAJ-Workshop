---
title: "Asynchronous Reporting Workflow"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5 </b> "
---

# Build Asynchronous Reporting Workflows with Step Functions, SQS & SES

In large enterprise applications, aggregating monthly timekeeping data across thousands of employees can take anywhere from 10 to 60 seconds of compute time. Executing this synchronously over an API Gateway connection risks triggering an **HTTP Timeout (30s limit)** and freezing the user interface.

In this lab module, you will implement an asynchronous reporting solution combining **AWS Step Functions Express State Machine**, **Amazon SQS Queue Buffer**, **Amazon S3**, and **Amazon SES Email Worker**.

---

### 1. Decoupled Asynchronous Architecture Flow

```
[Admin Request] ➔ [API Gateway] ➔ [SQS ReportQueue] ➔ [Step Functions Engine]
                                                               │
                                                               ▼
[Amazon SES Email] ◄─ [Lambda Email Worker] ◄─ [Amazon S3 Bucket (Report PDF/Excel)]
```

1. **Trigger Request:** Admin clicks "Export Monthly Report". The React frontend sends an HTTP POST request to API Gateway. The request is immediately buffered into the **SQS ReportQueue**, returning a `202 Accepted` response instantly (UI remains responsive).
2. **State Machine Execution:** The **AWS Step Functions Express Workflow (`ReportStateMachine`)** consumes tasks from SQS, orchestrating a 5-step workflow:
   * `ValidateRequest`: Validates `yearMonth` and `tenantId` parameters.
   * `InitializeReportStatus`: Updates the report status to `PROCESSING` in DynamoDB.
   * `GenerateReportFile`: Triggers a Lambda function to query attendance logs and build Excel/PDF binaries.
   * `WriteFileToS3`: Writes generated report files directly to an **Amazon S3 Bucket (`SaaSReportBucket`)** encrypted with KMS CMK and lifecycle managed via **S3 Intelligent-Tiering**.
   * `FinalizeReportStatus`: Updates report status to `COMPLETED` and attaches the S3 Key reference in DynamoDB.
3. **Notification Event:** EventBridge captures the `ReportGenerated` event, dispatching a notification message to **SQS EmailQueue**. The **Lambda Email Worker** processes queue messages in batches, invoking **Amazon SES** to email secure download links to admins.

---

### 2. State Machine Infrastructure Definition (`template.yaml`)

Below is the Express State Machine definition declared within AWS SAM:

```yaml
ReportStateMachine:
  Type: AWS::Serverless::StateMachine
  Properties:
    Type: EXPRESS
    Role: !GetAtt ReportWorkflowRole.Arn
    Definition:
      StartAt: ValidateRequest
      States:
        ValidateRequest:
          Type: Pass
          ResultPath: "$.validation"
          Next: InitializeReportStatus
        InitializeReportStatus:
          Type: Task
          Resource: arn:aws:states:::dynamodb:putItem
          Parameters:
            TableName: !Ref SaaSAttendanceTable
            Item:
              PK: { S.$: '$.PK' }
              SK: { S.$: '$.SK' }
              Status: { S: "PROCESSING" }
          Next: GenerateReportFile
        GenerateReportFile:
          Type: Pass
          Result:
            S3Key: "reports/monthly-attendance-report.xlsx"
          ResultPath: "$.fileDetails"
          Next: WriteFileToS3
        WriteFileToS3:
          Type: Task
          Resource: arn:aws:states:::aws-sdk:s3:putObject
          Parameters:
            Bucket: !Ref SaaSReportBucket
            Key.$: '$.fileDetails.S3Key'
            Body: "Report Binary Content"
          Next: FinalizeReportStatus
        FinalizeReportStatus:
          Type: Task
          Resource: arn:aws:states:::dynamodb:updateItem
          Parameters:
            TableName: !Ref SaaSAttendanceTable
            Key:
              PK: { S.$: '$.PK' }
              SK: { S.$: '$.SK' }
            UpdateExpression: "SET #status = :val, #file = :file"
            ExpressionAttributeNames:
              "#status": "Status"
              "#file": "ReportFileKey"
            ExpressionAttributeValues:
              ":val": { S: "COMPLETED" }
              ":file": { S.$: '$.fileDetails.S3Key' }
          End: true
```

---

### 3. SQS Queue & Dead Letter Queue (DLQ) Setup

To guarantee notification delivery resilience against network faults or SES sandbox rate limits, the queue architecture incorporates a **Dead Letter Queue (DLQ)** pattern:

```yaml
EmailQueue:
  Type: AWS::SQS::Queue
  Properties:
    QueueName: smart-attendance-email-queue
    RedrivePolicy:
      deadLetterTargetArn: !GetAtt EmailDLQ.Arn
      maxReceiveCount: 3

EmailDLQ:
  Type: AWS::SQS::Queue
  Properties:
    QueueName: smart-attendance-email-dlq
```

* If message processing fails 3 consecutive times in the worker Lambda, SQS automatically isolates failed messages in **EmailDLQ** for inspection without message loss.
