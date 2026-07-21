---
title: "Event 1"
date: "2024-01-01"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Summary Report: “FCAJ Community Day"

### Key Objectives
Master Modern Architecture: Gain a comprehensive understanding of how cloud-native applications are designed, decoupled, and modernized on AWS.
Shift to Business-First Design: Move beyond service-level features to focus on system design, domain modeling, and asynchronous event flows.
Integrate AI into the SDLC: Explore how AI tools like Amazon Q Developer enhance engineering productivity across code generation, refactoring, and documentation.

### Key Highlights
Domain-Driven Design (DDD): Emphasized starting system architecture by understanding business domain requirements and event triggers rather than database schemas.

Event-Driven Architecture (EDA): Demonstrated how asynchronous communication reduces tight coupling between services, improving system elasticity and fault tolerance.

Serverless Computing: Traced the progression from virtual servers (EC2) to containers and AWS Lambda, showing how serverless removes infrastructure management overhead.

Amazon Q Developer: Showcased practical AI workflows for accelerating boilerplate coding, generating technical documentation, and assisting in modernizing legacy applications.

Strategic Modernization: Highlighted that app modernization should follow an iterative, incremental roadmap rather than a risky full-scale rebuild.

### Key Takeaways
Architecture Precedes Code: Understanding the business domain is the bedrock of system design; CSDL models and API endpoints should follow business requirements, not lead them.

Decoupling Enables Scale: Asynchronous event streams prevent cascading failures and allow individual microservices to scale independently during traffic bursts.

Infrastructure Automation: Serverless shifts engineer focus toward core business logic, maximizing developer velocity and operational efficiency.

AI as a Productivity Co-Pilot: Generative AI tools accelerate routine software engineering tasks, but human architectural oversight remains essential.

### My Experience
Attending this workshop was a major turning point in my mindset as a software developer. Prior to this session, my instinct when building a project was to dive straight into designing CSDL tables and API routes. Seeing how enterprise systems leverage Domain-Driven Design completely transformed how I analyze software problems.
The sessions provided a clear, real-world perspective on why modern cloud architectures are shifting toward serverless and event-driven patterns. Overall, the experience helped me transition from thinking merely as a coder to viewing software through the lens of a Cloud Solutions Architect.

### Applying to Project
I am directly incorporating these learnings into my current AWS Event Management Platform:
Refactoring Domain Flows: Before writing backend services, I mapped out the core business journey into discrete domain events: Event Registration, Ticket Generation, Attendance Tracking, and Certificate Issuance.
Serverless & Event-Driven Stack: I reaffirmed my stack choice using Amazon API Gateway, AWS Lambda, and Amazon DynamoDB. Adding asynchronous event queues ensures that high-volume ticket releases won't overload dependent services.
AI-Assisted Workflow: I am leveraging AI tools to draft unit tests, format API documentation, and troubleshoot code, while enforcing strict human code reviews before pushing to production.

