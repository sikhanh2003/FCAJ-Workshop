---
title: "Preparation Steps"
date: "2024-01-01"
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

# Environment Prerequisites & Setup

Before starting the hands-on deployment of the **Smart Attendance SaaS Platform**, ensure your local development environment or AWS Cloud9 workspace is configured with the necessary tools and credentials.

---

### 1. Required Tooling Setup

Verify that the following CLI tools are installed on your workstation:

* **AWS CLI (v2.x):** Command-line interface for communicating with AWS services.
  ```bash
  aws --version
  ```
* **AWS SAM CLI:** Tool for building, testing, and deploying Serverless applications.
  ```bash
  sam --version
  ```
* **Node.js (v20.x+) & npm:** JavaScript runtime for Lambda microservices & React SPA frontend.
  ```bash
  node -v
  npm -v
  ```
* **Git:** Source control management.
  ```bash
  git --version
  ```

![CLI Tools Version Check Output](/images/5-Workshop/5.2-Prerequisite/check_version_installation.png)

---

### 2. Step-by-Step IAM User & Access Key Creation

Following AWS security best practices, never use the AWS Root Account for hands-on labs. Create a dedicated **IAM User** with administrator permissions:

#### Step 2.1: Create IAM User in AWS Console
1. Log in to the [AWS IAM Console](https://console.aws.amazon.com/iam/).
2. In the left navigation pane, select **Users** ➔ Click **Create user**.
3. Specify user details:
   * **User name:** `WorkshopAdmin` (or a custom name).
   * **Provide user access to the AWS Management Console:** *Optional if Web Console access is required*.
4. Click **Next**.

#### Step 2.2: Attach Permissions
1. Under **Permissions options**, select **Attach policies directly**.
2. Search and select the managed policy: `AdministratorAccess` *(Required for SAM CLI to provision CloudFormation stacks, IAM Roles, Lambda, DynamoDB, API Gateway, Cognito, S3, CloudFront, SQS, Step Functions, etc.)*.
3. Click **Next** ➔ Review details ➔ Click **Create user**.

#### Step 2.3: Generate Access Key ID & Secret Access Key
1. Click on your newly created user (`WorkshopAdmin`) in the **Users** table.
2. Select the **Security credentials** tab.
3. Scroll down to the **Access keys** panel ➔ Click **Create access key**.
4. Select the use case: **Command Line Interface (CLI)**.
5. Check the confirmation checkbox *"I understand the above recommendation and want to proceed to create an access key."* ➔ Click **Next**.
6. (Optional) Set a description tag (e.g., `AWS CLI for Workshop`) ➔ Click **Create access key**.
7. **CRITICAL:** Download the `.csv` file containing the **Access Key ID** and **Secret Access Key** immediately. *(You will not be able to view the Secret Access Key again after closing this window)*.

---

### 3. Configure AWS CLI Credentials

Once your Access Keys are created, open your terminal and execute:

```bash
aws configure
```

Enter your credentials generated in Step 2.3:

```text
AWS Access Key ID [None]: AKIAXXXXXXXXXXXXXXXX
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: ap-southeast-1
Default output format [None]: json
```

Verify successful connection:

```bash
aws sts get-caller-identity
```

A JSON response displaying your `UserId` and `Arn` confirms your AWS CLI is successfully configured!

---

### 4. Clone Project Source Repository

Clone the project source repository into your working directory:

```bash
cd ~/Documents/AWS
git clone https://github.com/your-repo/smart-attendance-saas.git
cd smart-attendance-saas
```

Source project file structure:

```text
smart-attendance-saas/
├── backend/                  # Serverless Backend Infrastructure (AWS SAM)
│   ├── src/                  # Lambda microservice handler functions
│   ├── template.yaml         # AWS SAM Infrastructure Template
│   └── samconfig.toml        # Deployment parameter configurations
├── frontend/                 # React SPA Frontend (Vite + TailwindCSS)
│   ├── src/                  # Components and Dashboard pages
│   └── package.json          # Node dependencies
└── platform_architecture.drawio # System architecture diagram
```

You are now ready to proceed to the backend deployment module!
