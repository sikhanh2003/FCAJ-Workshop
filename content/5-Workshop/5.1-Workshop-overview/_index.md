---

title: "Introduction"
date: "2024-01-01"
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# Overview of the Smart Attendance SaaS Platform Workshop

### Introduction

In this lab, you will explore the big picture of building a multi-tenant timekeeping software-as-a-service (**SaaS**) platform powered 100% by the **AWS Serverless** ecosystem.

### System Architecture Diagram

Below is the complete serverless architecture model that you will build and deploy throughout this workshop series:

![Smart Attendance SaaS Architecture](/images/5-Workshop/5.1-Workshop-overview/platform_architecture.png)

### Key Objectives & Learning Outcomes

After completing this workshop, you will gain hands-on expertise in:

1. **Infrastructure as Code (IaC):** Defining and managing cloud infrastructure using **AWS SAM (Serverless Application Model)** via template code (`template.yaml`).
2. **Multi-Tenant Authentication:** Configuring **Amazon Cognito User Pool** with custom attributes (`tenantId`, `role`) and attaching it to **Amazon API Gateway HTTP API v2** via JWT Authorizer.
3. **Optimized NoSQL Database Modeling:** Designing a **Single-Table Design** on **Amazon DynamoDB**, enabling KMS CMK encryption and **DynamoDB Streams** for Change Data Capture (CDC).
4. **Asynchronous Event-Driven Workflows:** Integrating **EventBridge Pipe**, **AWS Step Functions Express Workflow**, **Amazon SQS**, and **Amazon SES** to automatically generate and deliver monthly PDF/Excel attendance reports via email.
5. **Web SPA Delivery & Edge Ingress Protection:** Hosting a React SPA on **Amazon S3**, delivering it globally via **Amazon CloudFront CDN**, and restricting API ingress using a Custom Verification Header (`x-origin-verify`).

### Estimated Duration

* **Estimated Time:** 60 - 90 minutes.
* **Level:** Intermediate to Advanced.

