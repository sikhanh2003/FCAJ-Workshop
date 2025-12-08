---
title: "Event 7"
date: "2024-01-01"
weight: 7
chapter: false
pre: " <b> 4.7. </b> "
---

# Summary Report: "AWS Cloud Mastery Series #2: DevOps on AWS"

### Event Objectives

- Understand the core mindset of DevOps beyond just tools and CI/CD pipelines
- Explore the "T-Shaped Skills" model for modern cloud engineers
- Deep dive into Infrastructure as Code (IaC) with CloudFormation and CDK
- Learn practical cost-optimization strategies for AWS Amplify and Database hosting
- Discover methods for testing infrastructure locally and visualizing metrics via CloudWatch

### Speakers

- **AWS FCAJ Team (First Cloud Journey)**
- **AWS Vietnam DevOps Specialists**

### Key Highlights

#### DevOps is a Mindset, Not Just Tools

One of the strongest opening points was that DevOps is fundamentally about culture. While tools are necessary, the collaboration between roles is what drives success.

- **T-Shaped Skills:** The session emphasized that engineers should go deep in one area (vertical bar) but possess broad enough knowledge (horizontal bar) to collaborate effectively across the team.
- **Roles & Collaboration:** Gained a clearer picture of how different DevOps roles interact in real-world projects, moving beyond theory to practical teamwork.

#### Practical Infrastructure & Tooling Insights

The workshop went beyond standard definitions to provide specific, "in-the-trenches" tips:

- **IaC Choices:** Reinforced the use of CloudFormation and AWS CDK for clean, repeatable infrastructure management.
- **Amplify Strategy:** A key highlight was the architectural decision to host Frontend on Amplify while managing the Backend via CloudFormation (instead of a full-stack Amplify deploy) for better control and cost management.

### Agenda

#### **Morning Session (8:00 AM – 12:00 PM)**

- **8:00 – 9:00 AM** | Welcome & DevOps Culture

  - Defining DevOps: Mindset vs. Toolset
  - The T-Shaped Skills model for developers
  - Understanding DevOps roles in a project team

- **9:00 – 10:30 AM** | _CI/CD & Pipeline Fundamentals_

  - Overview of CI/CD pipelines
  - Clarification: Why DevOps is more than just CI/CD
  - **Demo:** Pipeline walkthrough

- **10:30 – 10:45 AM** | Break

- **10:45 AM – 12:00 PM** | _Infrastructure as Code (IaC)_

  - CloudFormation vs. Terraform (Concept comparison)
  - Using AWS CDK for programmable infrastructure
  - **Tip:** Testing infrastructure before cloud deployment to reduce development costs

- **12:00 – 1:00 PM** | Lunch Break

---

#### **Afternoon Session (1:00 PM – 4:00 PM)**

- **1:00 – 2:30 PM** | _Advanced Hosting & Compute Services_

  - AWS Amplify deeply explored
  - Architecture Tip: FE on Amplify + BE via CloudFormation/CDK
  - Database Hosting: Using EC2 for databases vs. RDS (Specific use cases)

- **2:30 – 2:45 PM** | Break

- **2:45 – 4:00 PM** | _Monitoring & Observability_

  - CloudWatch deeper dive
  - **Technique:** Embedding CloudWatch metrics directly into App UI (In-app dashboards)
  - Q&A & Wrap-up

### Key Takeaways

#### Strategic Insights into DevOps Culture

- **Culture First:** DevOps is a combination of culture, tools, and operational discipline. The mindset shift is as critical as the technical implementation.
- **Skill Development:** Adopting the T-Shaped skill set is essential for career growth and effective team collaboration.
- **Scope:** DevOps is much broader than just setting up a CI/CD pipeline; it encompasses the entire lifecycle and feedback loops.

#### Practical Technical Tips (The "Hidden Gems")

- **Cost Optimization with Amplify:** It is often more cost-effective and flexible to separate the Frontend (Amplify) from the Backend (CloudFormation/CDK) rather than relying on Amplify's "magic" for everything.
- **Database Flexibility:** While RDS is standard, there are legitimate scenarios where hosting a database on EC2 is a viable strategy for specific constraints.
- **Local Testing:** Infrastructure code can and should be tested before deployment. This practice significantly reduces cloud costs during the development phase.
- **Enhanced Observability:** We can leverage CloudWatch to create in-app dashboards, exposing relevant metrics directly to the user or admin UI, not just the AWS Console.

### Applying to Work

- **Adopt T-Shaped Learning:** Focus on deepening my core expertise while actively learning adjacent technologies to better support my team.
- **Refine IaC Workflow:** Implement local infrastructure testing in my current workflow to minimize wasted cloud resources.
- **Architecture Decisions:** Re-evaluate current projects to see if the "Amplify FE + Custom BE" pattern can optimize costs.
- **Dashboarding:** Experiment with pulling CloudWatch metrics into the application frontend for better operational visibility.

### Event Experience

This session by the AWS FCAJ team was incredibly clear and practical. It successfully bridged the gap between high-level DevOps concepts and actionable engineering tactics.

#### Learning from the Experts

- The speakers provided "real talk" about architecture, such as when *not* to use certain managed services (like full-stack Amplify) if it doesn't fit the budget or control requirements.
- The breakdown of the T-Shaped model gave me a clear direction for my personal professional development.

#### Practical Applicability

- The tip about testing infrastructure locally was a game-changer for my development workflow.
- Visualizing CloudWatch data inside the app is a feature I plan to implement immediately.

<!-- <div style="text-align: center;">
  {{< figure src="/images/Events/event6.1.jpg">}}
</div>

<div style="text-align: center;">
  {{< figure src="/images/Events/event6.2.jpg">}}
</div>

<div style="text-align: center;">
  {{< figure src="/images/Events/event6.3.jpg">}}
</div>

<div style="text-align: center;">
  {{< figure src="/images/Events/event6.4.jpg">}}
</div>

<div style="text-align: center;">
  {{< figure src="/images/Events/event6.5.jpg">}}
</div> -->

> Overall, this session strengthened my understanding of DevOps foundations. It clarified that while CI/CD is the engine, the culture and architectural choices (like IaC and observability) are the steering wheel.