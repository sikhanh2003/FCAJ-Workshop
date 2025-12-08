---
title: "Event 6"
date: "2024-01-01"
weight: 6
chapter: false
pre: " <b> 4.6. </b> "
---

# Summary Report: "AWS Cloud Mastery Series #1: AI/ML/GenAI on AWS"

### Event Objectives

* Provide a practical and strategic overview of AI/ML and Generative AI capabilities on AWS
* Demonstrate how foundation models and pretrained services can be integrated into enterprise solutions
* Introduce best practices in prompt engineering, RAG (Retrieval-Augmented Generation), and orchestration for production use
* Expose participants to AWS tools for accelerating AI adoption, including Bedrock and related services
* Equip attendees with actionable guidance for designing scalable, responsible, and cost-effective AI systems on the cloud

### Speakers

* AWS Cloud Mastery Series instructors and engineers (AWS Vietnam office)
* Workshop facilitators and technical demonstrators for Amazon Bedrock and SageMaker

### Key Highlights

#### Overview of AWS AI/ML Ecosystem

The workshop began with a structured overview of AWS’s AI/ML offerings, clarifying how managed services, foundation-model hosting, and orchestration layers fit together. Attendees received a map of the stack: pretrained services for rapid prototyping, managed ML platforms for training and deployment, and foundation-model hosting for advanced GenAI scenarios.

#### Generative AI with Amazon Bedrock

A major portion of the session focused on Amazon Bedrock and enterprise GenAI design patterns:

* Comparison and selection strategies for foundation models (Claude, Llama, Titan) with trade-offs in cost, latency, reasoning style, and enterprise suitability.
* Best practices in prompt engineering: structured prompts, chain-of-thought reasoning, and few-shot techniques to improve reliability and control.
* Retrieval-Augmented Generation (RAG) architecture: integrating knowledge bases to ground model outputs and improve factuality.
* Bedrock Agentcore: orchestrating multi-step workflows and tool-augmented reasoning to support more complex application flows.

#### Pretrained AI Services and Practical Tooling

The workshop covered AWS’s pretrained services that speed development without full model training:

* Amazon Comprehend — text analytics and NLP
* Amazon Rekognition — image and video analysis
* Amazon Textract — document extraction and OCR
* Amazon Translate / Transcribe / Polly — translation, speech-to-text, and text-to-speech
* Amazon Kendra — enterprise search
* Amazon Personalize — personalization and recommendations

The instructors emphasized when to use pretrained services versus custom models and how to combine them with Bedrock for hybrid solutions.

### Event Agenda Overview

- **8:30 AM – 9:00 AM** | Welcome & Introduction

  - Participant registration and networking
  - Workshop overview and learning objectives
  - Ice-breaker activity
  - Overview of Vietnam’s AI/ML landscape

- **9:00 AM – 10:30 AM** | _AWS AI/ML Services Overview_

  - Amazon SageMaker: End-to-end ML platform
  - Data preparation and labeling workflows
  - Model training, tuning, and deployment
  - Integrated MLOps capabilities
  - **Live Demo:** SageMaker Studio walkthrough

- **10:30 AM – 10:45 AM** | Coffee Break

- **10:45 AM – 12:00 PM** | _Generative AI with Amazon Bedrock_

  - Foundation Models: Claude, Llama, Titan – comparison & selection guide
  - Prompt engineering: Chain-of-thought, few-shot prompting
  - Retrieval-Augmented Generation (RAG) architecture & knowledge base design
  - Bedrock Agents for multi-step workflows and tool integrations
  - Guardrails configuration for safe and controlled AI output
  - **Live Demo:** Building a Generative AI chatbot using Bedrock

- **12:00 PM** | Lunch Break (Self-arranged)
### Key Takeaways

#### Technical Patterns & Best Practices

* Adopt a layered AI stack: pretrained services for quick wins, SageMaker for model lifecycle management, and Bedrock for foundation-model use cases.
* RAG is essential for enterprise-grade GenAI: it grounds generation in verified documents and reduces hallucination risk.
* Prompt engineering materially affects quality and cost — structuring prompts for concise, focused responses saves inference time and improves reliability.
* Orchestration (Agentcore) enables multi-step reasoning and tool use, allowing models to interact with databases, APIs, and other services safely.

#### Operational & Governance Considerations

* Data governance, access control, and explainability must be integrated from design time — not added later.
* Monitor inference cost and latency trade-offs when choosing foundation models; smaller/lightweight models can be used where latency and cost matter most.
* Implement logging, auditing, and evaluation pipelines to verify model outputs and track drift over time.

### Applying to Work

* Start small: prototype with pretrained services and a minimal RAG pipeline before investing in heavy model training.
* Use S3 for content storage and implement a search/index (e.g., Kendra or OpenSearch) to back RAG retrieval.
* Orchestrate multi-step flows with Agentcore or Lambda-based controllers for deterministic, auditable behavior.
* Add CI/CD for model artifacts and prompt/version management to ensure reproducibility.
* Define metrics for quality, latency, and cost; instrument systems with CloudWatch and regular evaluation jobs.

### Event Experience

Attending the AWS Cloud Mastery Series #1 workshop offered a balanced mix of conceptual framing and practical techniques. The sessions helped translate abstract GenAI ideas into concrete engineering patterns that can be applied in real projects.

#### What I Learned from the Event

* A clear mental model of the AWS AI/ML stack and when to choose each component
* Practical prompt engineering techniques that improve output quality and reduce cost
* How RAG pipelines and knowledge-base integration substantially improve trustworthiness of generative answers
* Orchestration approaches for multi-step reasoning and tool integration using Bedrock Agentcore

#### Networking & Community

* Connected with practitioners and AWS engineers at the Vietnam office, gaining pointers to documentation, sample repos, and follow-up labs
* Learned about additional workshops and community resources to continue hands-on practice

> The workshop provided an essential bridge between theoretical generative AI concepts and production-ready engineering patterns on AWS. It clarified practical next steps for designing scalable, responsible, and cost-aware AI systems.
