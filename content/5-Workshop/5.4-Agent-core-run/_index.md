---
title: "DynamoDB Single-Table Design"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4 </b> "
---

# DynamoDB Single-Table Design & DynamoDB Streams CDC

In a Multi-Tenant SaaS platform, database architecture directly dictates **infrastructure cost**, **query performance**, and **Tenant Data Isolation**.

In this module, you will explore the **Single-Table Design** pattern on Amazon DynamoDB and Change Data Capture (CDC) with **DynamoDB Streams**.

---

### 1. Single-Table Schema Layout

Instead of provisioning separate databases or tables per tenant/entity (Users, Attendance, Tenants, Subscriptions), all entities are co-located within a **Single Table (`smart-attendance-database`)** using HASH (`PK`) & RANGE (`SK`) design:

| Entity Type | Partition Key (`PK`) | Sort Key (`SK`) | Attributes |
| :--- | :--- | :--- | :--- |
| **Tenant Record** | `TENANT#<tenantId>` | `METADATA` | `tenantName`, `plan`, `status`, `createdAt` |
| **User Profile** | `TENANT#<tenantId>` | `USER#<userId>` | `email`, `fullName`, `role`, `department` |
| **Attendance Log** | `TENANT#<tenantId>` | `ATTENDANCE#<userId>#<timestamp>` | `checkInTime`, `checkOutTime`, `status`, `location` |
| **Subscription Billing**| `TENANT#<tenantId>` | `SUB#<billingId>` | `planTier`, `amount`, `paymentStatus`, `expiryDate` |

#### Ironclad Tenant Data Isolation
* Every Lambda database query **must** explicitly scope requests using the Partition Key prefix `TENANT#<tenantId>`.
* Guarantees 100% isolation against cross-tenant data leakage risks.

---

### 2. Inspect DynamoDB Table via AWS Console

1. Open the [Amazon DynamoDB Console](https://console.aws.amazon.com/dynamodbv2/).

![Amazon DynamoDB Console Dashboard](/images/5-Workshop/5.4-DynamoDB-SingleTable/access_amazon_dynamodb.png)

2. Select **Tables** -> Choose `smart-attendance-database`.
3. Review the **Overview** section:
   * **Read/Write capacity mode:** `On-Demand` (scales throughput automatically).

![Check On-Demand Capacity Mode](/images/5-Workshop/5.4-DynamoDB-SingleTable/check_capacity_mode.png)

   * **Encryption:** `KMS` (encrypted using Customer Managed Key `DataKMSKey`).
   * **Point-in-time recovery (PITR):** `ENABLED`.

![Check Point-in-Time Recovery (PITR)](/images/5-Workshop/5.4-DynamoDB-SingleTable/check_pirt.png)

   * **DynamoDB Streams:** `ENABLED (NEW_AND_OLD_IMAGES)`.

![Check DynamoDB Streams Status](/images/5-Workshop/5.4-DynamoDB-SingleTable/check_dynamo_stream.png)

---

### 3. EventBridge Pipe Integration for CDC

To process database mutations asynchronously without blocking the Check-in API latency, the solution connects DynamoDB Streams to EventBridge using **AWS EventBridge Pipes**:

```yaml
DdbToEventBridgePipe:
  Type: AWS::Pipes::Pipe
  Properties:
    Name: smart-attendance-ddb-stream-pipe
    Source: !GetAtt SaaSAttendanceTable.StreamArn
    Target: !Sub 'arn:aws:events:${AWS::Region}:${AWS::AccountId}:event-bus/default'
```

* When a new clock-in entry is committed to DynamoDB, **DynamoDB Streams** captures the change record.
* **EventBridge Pipe** routes the `AttendanceCreated` event directly to the **EventBridge Event Bus**, triggering background notification workers or third-party webhooks seamlessly.

