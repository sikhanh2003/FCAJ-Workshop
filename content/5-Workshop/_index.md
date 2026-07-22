---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Building a Multi-Tenant Smart Attendance Platform with AWS Serverless Architecture

#### Overview

In this hands-on Workshop series, you will step-by-step build and deploy a complete **Smart Attendance SaaS Platform** engineered for multi-tenant organizations using **AWS Serverless Optimized Pro Architecture**.

You will directly practice Infrastructure as Code (IaC) with **AWS SAM (Serverless Application Model)**, configure identity authentication with **Amazon Cognito User Pool**, model data with **Amazon DynamoDB (Single-Table Design)** enforcing tenant isolation via `tenantId`, implement **AWS Step Functions Express Workflows** and **Amazon SQS / SES** for asynchronous report generation, and deploy a React SPA frontend globally over **Amazon S3** and **Amazon CloudFront CDN** secured with Custom Origin Verification Headers.

#### Workshop Modules

1. [Workshop Overview](5.1-Workshop-overview/)
2. [Prerequisites](5.2-Prerequiste/)
3. [Deploy Serverless Backend with AWS SAM](5.3-Deploy-Backend/)
4. [DynamoDB Single-Table Design & DynamoDB Streams](5.4-DynamoDB-SingleTable/)
5. [Build Asynchronous Reporting Workflow](5.5-Async-Reporting/)
6. [Deploy React SPA Frontend & CloudFront CDN](5.6-Frontend-CloudFront/)
7. [End-to-End Testing & Resource Cleanup](5.7-Testing-Cleanup/)
