---
title: "Event 11"
date: "2024-01-01"
weight: 11
chapter: false
pre: " <b> 4.11. </b> "
---

# Summary Report: “BUILDING AGENTIC AI - Context Optimization with Amazon Bedrock”

### Event Objectives

- Understand the architecture and capabilities of **Amazon Bedrock AgentCore**.
- Explore the shift from simple chatbots to **Agentic Workflows** capable of complex reasoning and execution.
- Learn how to integrate external models and optimize context for high-performance AI agents.
- **Hands-on Workshop:** Experience using "Cloud Agents" (via CloudThinker) to connect, retrieve, and analyze AWS resources for actionable **Cost** and **Security** findings.

### Speakers

- **Mr. Nguyen Gia Hung** – Head of Solutions Architect, AWS
- **Mr. Kien Nguyen** – Solutions Architect, AWS
- **Mr. Viet Pham** – Founder & CEO (Shared real-world Agentic Workflow use cases)
- **CloudThinker Team:** Mr. Thang Ton (COO), Mr. Henry Bui (Head of Engineering)
- **Mr. Kha Van** – Community Leader (Led the Hands-on Workshop)

### Key Highlights

#### 1. Bedrock AgentCore: The Orchestration Engine
The session by **Mr. Kien Nguyen** provided a deep technical dive into **Amazon Bedrock AgentCore**.
- **Superior Integration:** I gained a clear understanding of why AgentCore stands out. It's not just about calling an LLM; it's about the ability to seamlessly **integrate external models** and route tasks effectively.
- **The "Core" Function:** It handles the heavy lifting of memory, prompt engineering, and API execution, allowing developers to focus on the business logic rather than the glue code.

#### 2. Building Real-World Agentic Workflows
**Mr. Viet Pham** showcased the journey of building an agentic workflow on AWS.
- Unlike theoretical examples, this session demonstrated the practical challenges and solutions in stringing together multiple agents to perform cohesive tasks.
- It bridged the gap between "having an LLM" and "having a functional automated worker."

#### 3. Deep Dive with CloudThinker & Cloud Agents
The core of the event for me was the introduction to **CloudThinker** and the concept of **Cloud Agents** presented by Mr. Thang Ton and Mr. Henry Bui.
- **Context Optimization:** Learned specifically how to optimize the context window (L300 level) so agents don't get overwhelmed when processing large amounts of infrastructure data.
- **Agentic Orchestration:** How multiple agents coordinate to understand the state of a cloud environment.

### Agenda

- **9:00 - 9:10** | Opening - *Nguyen Gia Hung*
- **9:10 - 9:40** | **AWS Bedrock AgentCore** - *Kien Nguyen*
    - Deep dive into AgentCore capabilities and external model integration.
- **9:40 - 10:00** | **[Use Case] Building Agentic Workflow on AWS** - *Viet Pham*
- **10:00 - 10:40** | **CloudThinker: Orchestration & Context Optimization**
    - Introduction by *Thang Ton*
    - Technical Deep Dive (L300) by *Henry Bui*
- **10:40 - 11:00** | Tea Break & Networking
- **11:00 - 12:00** | **CloudThinker Hack: Hands-on Workshop** - *Kha Van*
    - Connecting agents to AWS resources and analyzing for Cost/Sec optimization.
- **12:00 Onwards** | Networking & Lunch

### Key Takeaways

#### Technical Insight: AgentCore's Edge
The standout feature of Bedrock AgentCore is its robustness in **model orchestration**. It abstracts the complexity of connecting an LLM to external data sources and APIs. I clearly understood how it enables a "plug-and-play" approach for external models, which is a significant advantage over building custom orchestration layers from scratch.

#### Practical Application: The "Cloud Agent" Paradigm
The concept of using AI Agents to audit cloud infrastructure is a game-changer.
- Instead of manually checking dashboards, we treat the infrastructure state as "Context."
- The Agent retrieves the resource configuration, "reads" it against best practices, and generates findings.

#### Workshop Experience: From Retrieval to Findings
The hands-on session led by **Mr. Kha Van** and the CloudThinker team was incredibly practical.
- **Connection:** We successfully connected CloudThinker to our AWS environment.
- **Retrieval:** The agents fetched resource data (metadata, configurations).
- **Analysis:** The most impressive part was seeing the agents analyze this data to output specific **Cost Optimization** and **Security** recommendations. It wasn't generic advice; it was tailored to the actual resources we scanned.

### Applying to Work

- **Experiment with AgentCore:** Start prototyping internal tools using Bedrock AgentCore to leverage its external model integration capabilities.
- **Automated Auditing:** Explore the "Cloud Agent" approach for my own projects—building simple agents that can query AWS APIs and summarize the security posture or cost anomalies automatically.
- **Context Management:** Apply the context optimization techniques learned from Henry Bui's session to ensure my AI applications remain performant and cost-effective when handling large datasets.

### Event Experience

This event perfectly balanced theory and practice. Moving from Kien Nguyen's architectural overview of Bedrock AgentCore to seeing it applied in Viet Pham's workflow, and finally doing it myself with CloudThinker/Kha Van, solidified the knowledge.

The capability of **Cloud Agents** to autonomously scan, retrieve, and provide findings on Cost and Security is something I plan to investigate further. It proved that Agentic AI is ready for complex operations, not just conversation.

<!-- <div style="text-align: center;">
  {{< figure src="/images/Events/event11.1.jpg">}}
</div>

<div style="text-align: center;">
  {{< figure src="/images/Events/event11.2.jpg">}}
</div> -->

> **Final Thought:** Agentic AI is shifting from "Chatting with data" to "Acting on infrastructure." The ability to integrate external models and retrieve live cloud context is the key to unlocking this power.