---
title: "Event 8"
date: "2024-01-01"
weight: 8
chapter: false
pre: " <b> 4.8. </b> "
---

# Summary Report: “AWS Perimeter Protection Workshop 2025: CloudFront & Application Security Deep Dive”

### Event Objectives

- Explore the evolution of Amazon CloudFront from a CDN to a foundational Edge security layer
- Deep dive into the new "Fixed-Price CDN + Security Plan" regarding cost predictability
- Learn advanced Origin protection techniques using CloudFront VPC Origin (Origin Cloaking)
- Understand the defense-in-depth strategy using Shield (L3/L4) and WAF (L7)
- Master modern Bot Control techniques (Silent Challenge vs. CAPTCHA)

### Speakers

- **Mr. Nguyễn Gia Hưng** (CloudFront Session)
- **Mr. Julian Ju** (WAF Session)
- **Mr. Kevin Lim** (Lab Support)

### Key Highlights

#### A New Era: Predictable Pricing & Bundled Security

One of the biggest announcements discussed was the shift towards a predictable cost model. The upcoming **Fixed-Price CDN + Security Plan** (launching Nov 19, 2025) changes the game by:
- Eliminating "surprise bills" and overage fear.
- Bundling CloudFront, WAF, Shield, Route 53, Logging, and S3 credits into a single monthly fee.
- Allowing businesses to scale traffic without the linear cost increase typically associated with CDNs.

#### Multi-Layer Defense: From Edge to Origin

The workshop emphasized that security shouldn't just be at the app level, but rooted at the Edge.
- **DDoS Absorption:** Leveraging CloudFront’s 700+ PoPs to mitigate volumetric attacks.
- **Origin Cloaking:** A standout technical deep dive was using **CloudFront VPC Origin**. This allows ALBs to sit inside a Private Subnet, making them completely invisible to the public internet, accessible only via CloudFront.

### Agenda

#### **Morning Session (CloudFront & Pricing)**

- **8:30 – 9:00 AM** | Welcome & Context

  - The shift of security responsibilities to the Edge
  - Introduction to the new Fixed-Price model

- **9:00 – 10:30 AM** | _Amazon CloudFront Deep Dive_

  - **Technique:** Multi-layer caching (Origin Shield) and HTTP/3
  - **Cost Saving:** Zero-rated data transfer from AWS Origin to CloudFront
  - **Architecture:** Implementing CloudFront VPC Origin for true private subnets
  - **Demo:** CloudFront distribution setup

- **10:30 – 10:45 AM** | Break

#### **Midday Session (WAF & Shield)**

- **10:45 AM – 12:00 PM** | _AWS WAF & Application Protection_

  - WAF deployment strategies: Why **COUNT mode** is mandatory first
  - Handling AI & Evasive Bots
  - **Bot Control:** TLS fingerprinting & Client Interrogation
  - **Shield Advanced:** Cost Protection & SRT access

- **12:00 – 1:00 PM** | Lunch Break

---

#### **Afternoon Session (Security Architecture & Labs)**

- **1:00 – 2:30 PM** | _Hands-on Lab: Optimize & Secure Internet Web Application_

  - Implementing WAF rules
  - Configuring Origin Access Control (OAC)
  - Testing defense mechanisms against simulated attacks

- **2:30 – 2:45 PM** | Break

- **2:45 – 3:30 PM** | _Fun Quiz & Scenario Challenges_

  - Real-world security scenarios
  - Knowledge checks on caching and pricing bundles

- **3:30 – 4:00 PM** | Wrap-up & Q&A

### Key Takeaways

#### Strategic Insights: The "Fixed-Price" Game Changer

- The introduction of a subscription model for CDN + Security removes the biggest barrier for many enterprises: unpredictable costs.
- Security is no longer an add-on; with the new bundle, it is an integrated standard for all applications.

#### Technical Deep Dive: Origin Protection

- **Cloaking is King:** Moving the Application Load Balancer (ALB) into a private subnet and using CloudFront VPC Origin effectively removes the attack surface from the internet.
- **Protocol Efficiency:** Using HTTP/3 and QUIC not only improves speed but enhances connection reliability for users on unstable networks.

#### Technical Deep Dive: WAF & Bot Control

- **Smart Challenges:** The industry is moving away from annoying CAPTCHAs. The preferred method is **Silent Challenge**, requiring the client to perform a proof-of-work to receive a session token.
- **Deployment Safety:** Never turn on `BLOCK` immediately. Always run rules in `COUNT` mode to analyze traffic and tune logic to avoid false positives.

### Applying to Work

- **Pricing Review:** Evaluate current projects to see if the new Fixed-Price Plan offers better ROI than Pay-as-you-go.
- **Re-architect Networking:** Plan to migrate public ALBs to private subnets using CloudFront VPC Origin.
- **WAF Tuning:** Implement "Client Interrogation" (JavaScript injection) to validate genuine browser behaviors against bots.
- **Incident Support:** Leverage Shield Advanced not just for DDoS protection, but for the "Cost Protection" feature to prevent billing spikes during attacks.

### Event Experience

This workshop was a masterclass in modern edge security. It clarified that CloudFront is no longer just for static content caching—it is the primary shield for the entire infrastructure.

#### Learning from the Masters

- It was inspiring to see **Mr. Julian Ju**, a technical expert with decades of experience (humbled age at almost 60), delivering deep insights with such energy.
- **Mr. Nguyen Gia Hung** acted as a true "sifu," breaking down complex networking concepts into understandable architectural patterns.
- **Kevin Lim** provided excellent support during the hands-on labs.

#### Key Lessons Learned

- **Predictability is Power:** Whether it's pricing or performance, the new AWS updates focus on removing volatility.
- **Identity at the Edge:** Modern WAF is about identifying *who* (or *what*) is connecting via fingerprinting, not just looking at IP addresses.

<!-- <div style="text-align: center;">
  {{< figure src="/images/Events/event8.1.jpg">}}
</div>

<div style="text-align: center;">
  {{< figure src="/images/Events/event8.2.jpg">}}
</div>

<div style="text-align: center;">
  {{< figure src="/images/Events/event8.3.jpg">}}
</div>

<div style="text-align: center;">
  {{< figure src="/images/Events/event8.4.jpg">}}
</div>

<div style="text-align: center;">
  {{< figure src="/images/Events/event8.5.jpg">}}
</div> -->

> Overall, this workshop gave me a clear roadmap for the future of CDN: It's Fixed-Price, it's Secure by Default, and it allows our Origin infrastructure to go completely dark to the public internet.