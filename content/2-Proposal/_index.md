---
title: "Proposal"
date: "2025-10-28"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# APT Magic  
## A Serverless AI Platform for Image Generation and Social Interaction

---

### 1. Executive Summary
**APT Magic** is a serverless AI-powered web application designed to enable users to generate, personalize, and share artistic content such as AI-generated images. The platform integrates with AI foundation models via **Amazon Bedrock** and provides a seamless web experience using **Next.js (SSR)** hosted on **AWS Amplify**.  

The MVP version focuses on real-time image generation and sharing, while the **Future Design** aims to scale with **SageMaker Inference**, **Step Functions**, and **AWS MLOps pipelines** for advanced model orchestration and automation.

APT Magic is developed as a modern, cost-efficient, and secure AWS-native architecture for small to medium user bases, with planned expansion into enterprise-grade AI orchestration.

---

### 2. Problem Statement
#### What’s the Problem?
Most AI image generation platforms are costly, rely on opaque third-party APIs, and offer limited personalization.  
Developers and creators often face high latency, lack of transparent model management, and limited control over user data security.

#### The Solution
APT Magic leverages **AWS serverless architecture** to deliver:
- Real-time AI image generation through **Amazon Bedrock Stability AI** models.  
- Secure user authentication and content management using **Amazon Cognito** and **DynamoDB**.  
- Scalable API handling via **AWS Lambda** and **API Gateway**.  
- Low-latency global delivery with **CloudFront CDN** and **WAF protection**.  

Future upgrades will include **Step Functions orchestration**, **SQS/SNS decoupling**, **SageMaker Inference pipelines**, and cost-efficient CI/CD via **CodeBuild**, **CodePipeline**, and **CloudFormation** — transforming APT Magic into a fully automated MLOps platform.

---

### 3. Solution Architecture

#### **MVP Architecture**
The MVP is a **fully serverless architecture**, focusing on scalability, maintainability, and cost-effectiveness.

**Core AWS Services:**
- **Route53 + CloudFront + WAF** — Secure global access and caching.
- **Amplify (Next.js SSR)** — Hosts the frontend and server-side rendering layer.
- **API Gateway + Lambda Functions** — Manage backend logic (image processing, subscription, post APIs).
- **Amazon Cognito** — User authentication and access control.
- **Amazon S3 + DynamoDB** — Data persistence and image storage.
- **Amazon Bedrock** — Integrates foundation model (Stability AI) for image generation.
- **Secrets Manager, CloudWatch, CloudTrail** — Security, logging, and monitoring.

**Security**
- **PrivateLink** for secure communication between Lambda and backend services.  
- **WAF + IAM policies** for traffic filtering and role-based access control.  

![APT Magic MVP Architecture](/AWS-FCJ-Workshop-2025/images/aptMagic_mvp.png)

---

#### **Future Design (Enhanced Architecture)**
APT Magic will evolve into an **AI orchestration platform**, introducing new layers for automation, resilience, and model lifecycle management.

**New Services to be Added:**
- **AWS Step Functions** — To orchestrate asynchronous workflows such as:
  - Multi-step AI image generation (prompt validation → inference → result upload).
  - Payment confirmation → model processing → notification.
- **Amazon SQS** — For reliable message queuing between async Lambda tasks.
- **Amazon SNS** — For real-time event notifications to users or administrators.
- **Amazon ElastiCache (Redis)** — For rate limiting and caching of frequent inference requests.
- **Amazon SageMaker Inference** — For hosting custom fine-tuned models and managing model endpoints.
- **AWS CodePipeline + SageMaker Pipelines** — To automate MLOps: model training, evaluation, and deployment.
- **AWS PrivateLink + VPC Endpoints** — For secure data flow between Lambda, S3, and SageMaker.
- **AWS WAF & Shield Advanced** — For DDoS protection and advanced security filtering.

**CI/CD + MLOps**
- **CodePipeline + CodeBuild + CloudFormation** for infrastructure deployment and automation.  

<!-- ![APT Magic Future Architecture](/images/aptMagic_future.png) -->

---

### 4. Technical Implementation

#### **Implementation Phases**
| **Phase** | **Duration** | **Key Deliverables** |
|------------|---------------|----------------------|
| **Phase 1 – MVP Deployment** | Month 1 | Amplify (Next.js SSR), API Gateway + Lambda, Bedrock integration, CI/CD setup (CodePipeline + CloudFormation), Cognito + S3 + DynamoDB |
| **Phase 2 – Expansion & Automation** | Month 2–3 | Add Step Functions, SQS/SNS orchestration, ElastiCache caching, integrate SageMaker Inference, enhanced CI/CD via CodeBuild |
| **Phase 3 – Scaling & Optimization** | Month 4+ | Implement SageMaker Pipelines, Shield Advanced, GuardDuty, PrivateLink, performance optimization and auto-scaling policies |

---

### 5. Timeline & Milestones
| **Milestone** | **Phase** | **Estimated Completion** | **Outcome** |
|----------------|-----------|---------------------------|--------------|
| MVP Launch | Phase 1 | Month 1 | Live platform with AI image gen & sharing |
| Async Workflow Integration | Phase 2 | Month 2 | Step Functions + SQS + SNS pipeline |
| MLOps Integration | Phase 2 | Month 3 | SageMaker Inference & CI/CD Automation |
| Scaling Optimization | Phase 3 | Month 4 | Secure, optimized infrastructure ready for growth |

---

### 6. Budget Estimation (AWS Pricing Estimate)

#### **MVP Estimated Cost (~$20/month)**
| Service | Est. Monthly Cost | Notes |
|----------|------------------|-------|
| AWS Amplify (Next.js SSR) | $0.40 | Hosting + build minutes |
| API Gateway | $0.09 | 25,000 requests/month |
| AWS Lambda | $0.21 | 25,000 invocations × 512MB × 1s |
| Amazon Bedrock | $3.00 | 5,000 image generations |
| DynamoDB | $0.30 | 1M reads, 100K writes, 1GB storage |
| S3 | $0.46 | 10GB storage + 10GB transfer |
| Cognito | $5.50 | 1,000 MAU |
| CloudFront | $1.70 | 20GB data transfer |
| WAF (Basic) | $6.00 | 1 WebACL + 5 rules |
| CloudWatch + Secrets Manager + CloudTrail | $2.30 | Logs, monitoring, secret management |
| **Total (MVP)** | **≈ $20.00/month** | Small-scale deployment |

#### **Future Design (Scalable MLOps – $45–60/month)**
| Service | Est. Monthly Cost | Notes |
|----------|------------------|-------|
| Step Functions + SQS + SNS | $0.60 | Async orchestration |
| ElastiCache (Redis) | $1.00 | Rate limiting / cache |
| SageMaker Inference | $5.00 | Managed endpoint cost |
| CodePipeline + CodeBuild | $2.00 | CI/CD automation |
| Shield Advanced + GuardDuty | $10–15 | Advanced protection |
| PrivateLink + VPC Endpoints | $7.00 | Secure private traffic |
| **Total (Future)** | **≈ $45–60/month** | Based on scaling level |

---

### 7. Risk Assessment
| Risk | Impact | Probability | Mitigation |
|------|--------|-------------|-------------|
| AI model inference latency | Medium | High | Use ElastiCache + Step Functions for async handling |
| Cost increase from model calls | High | Medium | Bedrock usage control, SageMaker autoscaling |
| CI/CD misconfigurations | Medium | Low | CloudFormation rollback policies |
| Security vulnerabilities | High | Medium | WAF, GuardDuty, PrivateLink, IAM least privilege |
| Third-party API dependency | Medium | Medium | Bedrock fallback to S3-stored inference results |

---

### 8. Expected Outcomes
#### **Technical Outcomes**
- Complete serverless AI image generation workflow with secure CI/CD.
- Modular orchestration enabling rapid MLOps integration.
- Improved latency and reliability via caching and async workflows.

#### **Long-Term Value**
- A foundation for **AI as a Service (AIaaS)** platform expansion.  
- Ready-to-scale **MLOps framework** with automated retraining.  
- Reusable, cost-optimized AWS infrastructure for future AI products.

---
