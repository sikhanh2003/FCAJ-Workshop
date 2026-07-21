---
title: "Proposal"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# SMART ATTENDANCE SAAS PLATFORM
Local and Cloud-Ready Hybrid Solution for Smart Attendance and User Management
### 1. Project Summary
The Smart Attendance SaaS Platform is a comprehensive digital solution designed for tracking attendance, user registration, authentication, and report management. The project was researched and developed to streamline attendance tracking workflows, support role-based user management, and provide a user-friendly interface for modern organizations and academic or enterprise teams.

The system supports clean user workflows by separating pages and functionalities such as Login, Register, Checkout, and Dashboard/Attendance reports. The platform covers the core requirements of an attendance tracking system through interconnected components:

User Authentication & Registration: Manages user identity and account creation through dedicated registration and login interfaces.

Attendance Management: Allows users to perform check-in and checkout actions efficiently with real-time tracking capabilities.

Reporting & Exporting: Collects operational attendance data and supports reporting features to export logs and metrics.

The project utilizes a modern web-based architecture combining an HTML/CSS frontend with a Node.js and Express backend (server.js), structured cleanly with modular source files (src/handler/, src/shared/) to ensure maintainability and smooth local or cloud deployment.

### 2. Problem Statement
What is the problem?
Currently, many small and medium-sized teams or organizations still rely on manual tracking or fragmented tools when managing member attendance, leading to several drawbacks:

Difficulty tracking real-time status: Traditional manual methods lack instant verification mechanisms, causing confusion and inaccurate attendance records.

Complex authentication overheads: Managing user credentials and secure access without a streamlined system leads to security vulnerabilities and cumbersome user experiences.

Lack of unified reporting: Compiling attendance logs and generating reports manually consumes substantial administrative time and effort.

Infrastructure rigidity: Heavy or poorly configured deployment setups make local testing, debugging, and continuous development complicated.

### Solution
The platform provides a unified application that automates and simplifies attendance tracking touchpoints:

Streamlined Check-in/Check-out Workflows: Users can seamlessly interact via intuitive HTML interfaces (index.html, checkin.html, checkout.html) backed by robust server routes to record data instantly.

Structured Backend Processing: Powered by an Express-based server (server.js) equipped with CORS support and modular handlers (src/handler/attendance/checkin.js, src/handler/reports/export.js) for reliable request handling and data management.

Flexible Deployment and Configuration: Designed with clear separation between frontend views and backend services, allowing developers to easily switch and test between local development environments and cloud configurations.

Benefits and Value Delivered
Optimized Operational Workflow: Reduces administrative overhead by digitizing the entire attendance tracking and reporting pipeline.

High Extensibility and Clean Architecture: The modular separation of handlers, shared database configurations, and UI components allows for easy scaling and feature expansion.

Developer-Friendly Environment: Provides a clear project layout that supports seamless local execution, fast debugging, and straightforward integration with version control systems like Git.

---

### 3. Solution Architecture
### MVP Architecture
The MVP is designed with a fully serverless, highly scalable cloud architecture tailored for SaaS applications, leveraging AWS managed services as illustrated in the system topology.

Core AWS Services & Infrastructure:

Global Edge Services: Amazon Route 53 (DNS Resolution), Amazon CloudFront (Global CDN), AWS Shield (DDoS Protection), AWS WAF v2, and Amazon S3 (React SPA Hosting).

Authentication & API Layer: Amazon Cognito (User Auth, JWT Token, Tenant/Role Management), AWS Secrets Manager, and Amazon API Gateway (HTTP API v2, JWT Authorizer, Caching, Throttling).

Compute Layer (AWS Lambda & Step Functions): Lambda functions for Webhook, Check-in, Check-out, Attendance, Report, Admin, and Subscription processing, coupled with Amazon SQS (Queue + DLQ) and AWS Step Functions Workflow.

Data Layer: Amazon DynamoDB (Single-Table Design, Streams Enabled for Attendance, Users, Tenants), DynamoDB Streams, AWS KMS (Customer Keys for Data Encryption), and Amazon S3 (Report Storage for PDF, Excel, CSV).

Event-Driven & Notification Layer: Amazon EventBridge (Event Bus), Amazon SNS (Email Queue + DLQ Buffer), Lambda Email Worker, and Amazon SES (Email Delivery for Reports, Alerts, Invoices).

Operations Layer (Monitoring, Tracing & CI/CD): CloudWatch, AWS X-Ray, CloudFormation, CodePipeline, CodeBuild, and AWS Security Hub / GuardDuty.

![Architecture](/AWS-FCJ-Workshop-2025/images/2-Proposal/aptMagic_mvp.jpg)

---

### 4. Technical Implementation
### Implementation Phases
Phase 1 – MVP Deployment (Completed / Current)

Implement Global Edge Services (Route53, CloudFront, WAF, S3 SPA Hosting).

Configure Authentication & API Layer via Amazon Cognito and API Gateway.

Deploy Compute Layer using AWS Lambda functions and Step Functions workflow.

Establish Data Layer with Amazon DynamoDB Single-Table Design, S3 Report Storage, and KMS encryption.

Enable Event-Driven notifications via EventBridge, SNS, and SES.

Log and monitor via CloudWatch, X-Ray, and Security Hub.

Phase 2 – Future Design Expansion

Optimize asynchronous processing pipelines via SQS and SNS queues.

Enhance automated CI/CD deployment routines using CodePipeline and CodeBuild.

Scale automated security policies and threat detection via GuardDuty.

---

### 5. Timeline & Milestones

| Phase | Description |
|-------|-------------|
| **Week 7: Project Initiation & Feasibility** | Comprehensive SaaS requirements specification, feasibility study on multi-tenant isolation, and definition of functional metrics for smart attendance workflow. |
| **Week 8: Core Architecture & Flow Modeling** | High-availability serverless topology mapping, detailed sequence diagrams for check-in/check-out tracking, and secure tenant authentication flowcharts. |
| **Week 9: Infrastructure Provisioning** | Infrastructure-as-Code scripts (template.yaml) provisioning DynamoDB single-tables, KMS encryption keys, and S3 secure storage buckets. |
| **Week 10: Security & Gateway Implementation** | Configured Amazon Cognito user pools with JWT tokens, hardened API Gateway endpoints, and deployed AWS WAF v2 rules for rate-limiting and bot defense. |
| **Week 11: Backend & Business Logic Engineering** | Functional Lambda microservices for attendance processing, automated SQS/SNS messaging buffers, Step Functions report workflows, and SES notification templates. |
| **Week 12: Integration, Testing & Launch** | Performance stress tests across CloudFront edge locations, integrated CI/CD pipeline verification via CodePipeline, and complete operational handover documentation. |

---

### 6. Cost Estimate (AWS Pricing Estimate)

#### Total Cost
- **Monthly:** $13.50  
- **Upfront:** $0.00  
- **12 Months:** $162.00

---

#### Service Overview

| Service | Region | Monthly Cost | Upfront | 12-Month Cost | Notes |
|--------|---------|--------------|---------|---------------|-------|
| Amazon Route 53 | Asia Pacific (Singapore) | $0.50 | $0.00 | $6.00 | 1 Hosted Zone & domain resolution setup |
| Amazon CloudFront |	Asia Pacific (Singapore) |	$0.00 |	$0.00 |	$0.00 |	Global CDN distribution for React SPA |
| AWS WAF v2 |	Asia Pacific (Singapore) |	$6.00 |	$0.00 |	$72.00 |	1 Web ACL; rate limiting, bot control, and geo rules |
|Amazon S3 |	Asia Pacific (Singapore) |	$0.35 |	$0.00 |	$4.20 |	SPA hosting and intelligent-tiering report storage |
|Amazon Cognito |	Asia Pacific (Singapore) |	$0.00 |	$0.00 |	$0.00 |	User pool authentication (Within monthly free tier) |
|AWS Secrets Manager |	Asia Pacific (Singapore) |	$0.40 |	$0.00 |	$4.80 |	1 active secret with automatic credential rotation |
|Amazon API Gateway |	Asia Pacific (Singapore) |	$0.20 |	$0.00 |	$2.40 |	HTTP API v2 with JWT authorizer, caching, and throttling |
|AWS Lambda |	Asia Pacific (Singapore) |	$1.85 |	$0.00 |	$22.20 |	Compute layer for check-in/out, webhooks, and reporting |
|AWS Step Functions |	Asia Pacific (Singapore) |	$0.10 |	$0.00 |	$1.20 |	Workflows for asynchronous report orchestration |
|Amazon SQS |	Asia Pacific (Singapore) |	$0.00 |	$0.00 |	$0.00 |	Standard queues + DLQ buffers |
|Amazon DynamoDB On-Demand |	Asia Pacific (Singapore) |	$0.60 |	$0.00 |	$7.20 |	Single-table design, streams enabled, on-demand mode |
|AWS KMS |	Asia Pacific (Singapore) |	$1.00 |	$0.00 |	$12.00 |	1 Customer Managed Key (CMK) for data encryption |
|Amazon EventBridge |	Asia Pacific (Singapore) |	$0.00 |	$0.00 |	$0.00 |	Custom event bus routing |
|Amazon SNS |	Asia Pacific (Singapore) |	$0.00 |	$0.00 |	$0.00 |	Notification routing and email queue buffer |
|Amazon SES |	Asia Pacific (Singapore) |	$0.10 |	$0.00 |	$1.20 |	Outbound transactional emails (Reports, alerts, invoices) |
|CloudWatch, X-Ray & Security Hub |	Asia Pacific (Singapore) |	$2.40 |	$0.00 |	$28.80 |	Logs, metrics, distributed tracing, and security posture checks |
|Total (Estimate) |	— |	$13.50 |	$0.00 |	$162.00 |	Based on AWS Pricing Calculator |

---

### 7. Risk Assessment
| Risk | Impact | Probability | Mitigation |
|------|---------|-------------|-------------|
| API request throttling or latency | Medium | High | Use API Gateway caching and Lambda optimization |
| Cost increase from database traffic spikes | High | Medium | Utilize DynamoDB on-demand scaling with fine-grained partition keys |
| Pipeline deployment failures | Medium | Low | Use CloudFormation rollback policies and CodePipeline stages |
| Security vulnerabilities | High | Medium | Enforce WAF rules, IAM least privilege, KMS encryption, and Security Hub alerts |
| Third-party API dependency | Medium | Medium | Implement robust error handling with SQS DLQ buffers |

---

### 8. Expected Outcomes
### Technical Outcomes:
Complete serverless attendance tracking workflow backed by AWS managed services.

Highly scalable event-driven architecture with secure CI/CD and monitoring pipelines.

Improved reliability via isolated data layers and asynchronous SQS/Step Functions workflows.

### Long-Term Value:
A production-ready foundation for Enterprise SaaS Attendance & Management expansion.

Fully automated cloud infrastructure utilizing Infrastructure as Code (CloudFormation).

Robust, secure, and cost-optimized architecture ready for high-volume concurrent users.
---


