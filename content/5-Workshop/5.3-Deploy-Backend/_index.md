---
title: "Deploy Serverless Backend"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

# Deploy Serverless Backend Infrastructure with AWS SAM & Cognito

In this module, you will package and deploy the complete Serverless Backend infrastructure using **AWS SAM (Serverless Application Model)**, including **Amazon Cognito User Pool**, **HTTP API Gateway v2**, **AWS Lambda** microservices, **Amazon DynamoDB Single-Table**, and **AWS KMS Keys**.

---

### 1. Inspect Infrastructure Code (`template.yaml`)

The `template.yaml` file specifies all cloud resources declaratively. Key components include:

* **Cognito User Pool (`CognitoUserPool`):** Manages user registration, authentication, and JWT issuing. Defines custom schema attributes `tenantId` and `role` to support multi-tenancy.
* **HTTP API Gateway (`AttendanceApi`):** Configures `CognitoAuthorizer` using OAuth2/JWT standard pointing to the Cognito User Pool issuer URL.
* **KMS Key (`DataKMSKey`):** Customer Managed Key (CMK) for data-at-rest encryption across DynamoDB and S3 buckets.
* **DynamoDB Table (`SaaSAttendanceTable`):** Single-Table Design schema with `PK` partition key and `SK` sort key, On-Demand billing, and DynamoDB Streams enabled.
* **Lambda Microservices:**
  * `AuthFunction`: Handles login, registration, and token exchange (`/auth/*`).
  * `CheckInFunction`: Records employee clock-in events (`/attendance/check-in`).
  * `CheckOutFunction`: Records employee clock-out events (`/attendance/check-out`).
  * `AttendanceHistoryFunction`: Queries attendance logs (`/attendance/history`).
  * `AdminFunction`: Handles admin management and company metrics (`/admin/*`).
  * `ReportFunction`: Handles async report creation requests.
  * `WebhookFunction`: Processes external payment webhooks and system alerts.

---

### 2. Build Infrastructure Artifacts (`sam build`)

Navigate to the `backend/` directory and execute the build command:

```bash
cd backend
sam build
```

Expected build confirmation:

```text
Build Succeeded

Built Artifacts  : .aws-sam/build
Valid Templates  : .aws-sam/build/template.yaml
```

![sam build execution result](/images/5-Workshop/5.3-Deploy-Backend/sam_build.png)

---

### 3. Deploy Cloud Infrastructure (`sam deploy`)

Execute the guided deployment command:

```bash
sam deploy --guided
```

Provide the deployment parameters when prompted:

```text
Configuring SAM deploy
======================

	Stack Name [sam-app]: smart-attendance-backend
	AWS Region [us-east-1]: us-east-1
	Parameter AllowedOrigin [https://your-cloudfront-domain.cloudfront.net]: https://localhost:3000
	Parameter OriginVerifySecret [SaaS-Secure-Verification-Token-2026]: SaaS-Secure-Verification-Token-2026
	Confirm changes before deploy [Y/n]: n
	Allow SAM CLI IAM role creation [Y/n]: Y
	Disable rollback [y/N]: N
	Save arguments to configuration file [Y/n]: Y
	SAM configuration file [samconfig.toml]: samconfig.toml
	SAM configuration environment [default]: default
```

CloudFormation stack creation takes approximately 2–3 minutes.

![sam deploy execution result](/images/5-Workshop/5.3-Deploy-Backend/sam_deploy.png)

> [!TIP]
> **Troubleshooting `Error: S3 Bucket does not exist`:**  
> This error occurs when the SAM CLI managed CloudFormation stack (`aws-sam-cli-managed-default`) still exists while its underlying S3 bucket was deleted manually. Delete the stale managed stack with:
> ```bash
> aws cloudformation delete-stack --stack-name aws-sam-cli-managed-default --region ap-southeast-1
> ```
> Then re-run `sam deploy --guided` to let SAM CLI create a clean, brand-new S3 Deployment Bucket.

---

### 4. Capture Stack Outputs

Upon successful deployment, SAM CLI displays the stack `Outputs`:

```text
Key                 AttendanceApiUrl
Description         API Endpoint URL
Value               https://xxxxxxx.execute-api.us-east-1.amazonaws.com/prod

Key                 CognitoUserPoolId
Description         Cognito User Pool ID
Value               us-east-1_xxxxxxxxx

Key                 CognitoUserPoolClientId
Description         Cognito App Client ID
Value               xxxxxxxxxxxxxxxxxxxxxxxxxx
```

> [!IMPORTANT]
> Save the `AttendanceApiUrl`, `CognitoUserPoolId`, and `CognitoUserPoolClientId` values. You will need them to configure the React SPA frontend in subsequent modules!
