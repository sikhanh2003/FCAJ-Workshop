---
title: "Testing & Resource Cleanup"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# End-to-End Testing & Resource Cleanup

Congratulations on building and deploying the complete **Smart Attendance SaaS Platform**! In this final module, you will perform end-to-end operational testing across 5 realistic scenarios and properly teardown deployed cloud resources to prevent ongoing AWS billing.

---

### 1. End-to-End Testing Scenarios

Follow these 5 test scenarios on your live application:

#### Scenario 1: Tenant Registration & Authentication (Multi-Tenant Auth)

1. Navigate to your CloudFront distribution URL.
2. Select **Register Tenant**. Enter Company A credentials (`tenantId`: `tenant-company-a`), Admin Email, and Password.
3. Complete email OTP verification.
4. Sign in as Admin. Verify the dashboard loads scoped under `tenant-company-a`.

#### Scenario 2: Employee Clock-In & Clock-Out

1. Create an Employee user (`user-employee-1`) associated with `tenant-company-a`.
2. Sign in as the employee on a mobile device or browser simulator.
3. Click **Clock-In** -> The app sends a JWT-authenticated request to API Gateway -> The `CheckInFunction` Lambda commits the entry in sub-200ms.
4. Click **Clock-Out** -> The system updates the clock-out timestamp in DynamoDB.

#### Scenario 3: Query Attendance History (DynamoDB Single-Table Query)

1. Open **Attendance History**.
2. The frontend queries DynamoDB using `TENANT#tenant-company-a` partition key, returning real-time attendance logs in sub-50ms.

#### Scenario 4: Export Monthly Attendance Reports (Step Functions & SES)

1. From the Admin Dashboard, click **Export Monthly Report**.
2. The UI displays an asynchronous confirmation status immediately ("Request Processing").
3. Inspect the AWS Step Functions Console to monitor the Express State Machine executing the report file generation.
4. Check your inbox for the automated email delivered via **Amazon SES** containing the secure download link from Amazon S3.

#### Scenario 5: B2B Subscription Payment Webhook

1. As Admin, select the Pro Tier plan and proceed to Checkout.
2. Simulate a payment gateway webhook callback to `/billing/webhook`.
3. The `WebhookFunction` validates the signature via **AWS Secrets Manager** and updates tenant status to `ACTIVE` in DynamoDB.

---

### 2. AWS Resource Cleanup & Teardown

To avoid unnecessary cloud costs after finishing the workshop, tear down all deployed resources following these steps:

#### Step 1: Empty S3 Bucket Contents

CloudFormation cannot delete non-empty S3 buckets. Empty bucket contents using the AWS CLI:

```bash
# 1. Purge S3 Report Bucket objects
aws s3 rm s3://saas-attendance-reports-<AWS_ACCOUNT_ID>-<REGION> --recursive

# 2. Purge S3 SPA Hosting Bucket objects
aws s3 rm s3://smart-attendance-spa-hosting-<AWS_ACCOUNT_ID> --recursive
```

#### Step 2: Delete CloudFormation Stack via SAM CLI

Change directory into `backend/` and execute the SAM delete command:

```bash
cd backend
sam delete
```

Confirm stack deletion prompts:

```text
Are you sure you want to delete the stack smart-attendance-backend in region us-east-1? [y/N]: y
Are you sure you want to delete the folder smart-attendance-backend in S3? [y/N]: y
```

CloudFormation takes approximately 3–5 minutes to destroy all resources (Cognito, API Gateway, Lambda, DynamoDB, Step Functions, SQS, SES, KMS Keys).

---

### Summary & Conclusion

Congratulations on completing the **Smart Attendance SaaS Platform Workshop**! You have mastered key **AWS Serverless** design patterns and gained practical experience engineering scalable multi-tenant SaaS platforms on AWS.
