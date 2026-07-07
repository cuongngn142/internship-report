---
title: 'Proposal'
date: 2026-07-07
weight: 2
chapter: false
pre: ' <b> 2. </b> '
---

# Security Operations Center (SOC) on AWS

## A Serverless Event-Driven Platform for Automated Threat Detection and Incident Response

### 1. Executive Summary

The Security Operations Center (SOC) on AWS is a serverless and event-driven security platform designed to automatically detect, analyze, and respond to cybersecurity threats in real time. The architecture follows the five core functions of the NIST Cybersecurity Framework: **Identify, Protect, Detect, Respond, and Recover**.

The solution protects cloud workloads deployed inside an Amazon VPC by integrating Amazon CloudFront, AWS WAF, AWS Shield Standard, Amazon GuardDuty, IAM Access Analyzer, AWS Security Hub, Amazon EventBridge, AWS Lambda, AWS Step Functions, Amazon SNS, Amazon Athena, and Amazon S3.

To optimize operational costs, the platform adopts FinOps principles by leveraging AWS Free Tier where possible, storing security logs in Amazon S3 instead of CloudWatch Logs, and querying data directly with Amazon Athena.

### 2. Problem Statement

#### What's the Problem?

Traditional security monitoring often relies on manual investigation and delayed incident response. Common challenges include:

- Lack of centralized security visibility.
- Slow threat detection.
- Manual incident response.
- High operational costs.
- Difficulty correlating security findings.

#### The Solution

The proposed SOC platform integrates AWS native security services into an automated security pipeline.

Incoming traffic is protected by Amazon CloudFront, AWS WAF and AWS Shield Standard before entering the Amazon VPC. AWS CloudTrail and Amazon VPC Flow Logs collect security events and store them centrally in Amazon S3 using AWS KMS encryption.

Amazon GuardDuty analyzes CloudTrail Management Events and VPC Flow Logs, while IAM Access Analyzer detects unintended resource exposure. AWS Security Hub aggregates findings and forwards them through Amazon EventBridge. Depending on severity, AWS Lambda or AWS Step Functions automatically isolate EC2 instances, block malicious IP addresses through AWS WAF IP Sets, revoke IAM Access Keys, generate incident reports in Amazon S3, and send notifications through Amazon SNS.

SOC analysts investigate incidents using Amazon Athena.

#### Benefits and Return on Investment

- Automated threat detection.
- Near real-time incident response.
- Reduced MTTD and MTTR.
- Centralized security monitoring.
- Lower operational costs through serverless architecture.
- Cost-efficient log storage using Amazon S3.

### 3. Solution Architecture

The architecture follows a layered defense-in-depth approach.

#### Architecture Layers

1. **Edge Protection** – Amazon CloudFront, AWS WAF and AWS Shield Standard protect against DDoS, SQL Injection, XSS and brute-force attacks.

2. **Network Isolation** – Amazon VPC contains a Public Subnet with an Application Load Balancer and NAT Instance (t4g.nano), while Amazon EC2 instances remain inside a Private Subnet protected by Security Groups.

3. **Data Collection** – AWS CloudTrail Management Events and Amazon VPC Flow Logs are stored in Amazon S3 using AWS KMS encryption.

4. **Storage** – Amazon S3 stores logs and incident reports with a 90-day Lifecycle Policy. Amazon Athena provides SQL-based investigation.

5. **Threat Detection** – Amazon GuardDuty, IAM Access Analyzer and AWS Security Hub detect and aggregate security findings.

6. **Automated Response** – Amazon EventBridge triggers AWS Lambda or AWS Step Functions to block IP addresses, isolate EC2 instances, revoke IAM credentials and notify SOC analysts.

7. **Monitoring Dashboard** – Amazon CloudWatch Dashboard displays findings, Lambda executions, blocked IPs and SNS notifications.

![SOC Architecture](/images/2-Proposal/aws_soc_architecture.png)

### AWS Services Used

| AWS Service                 | Purpose                  |
| --------------------------- | ------------------------ |
| Amazon CloudFront           | Edge protection          |
| AWS WAF                     | Web application firewall |
| AWS Shield Standard         | DDoS protection          |
| Amazon VPC                  | Network isolation        |
| Application Load Balancer   | Traffic distribution     |
| Amazon EC2                  | Protected workload       |
| AWS CloudTrail              | Management event logging |
| Amazon VPC Flow Logs        | Network traffic logging  |
| Amazon S3                   | Centralized log storage  |
| AWS KMS                     | Log encryption           |
| Amazon GuardDuty            | Threat detection         |
| IAM Access Analyzer         | IAM exposure analysis    |
| AWS Security Hub            | Findings aggregation     |
| Amazon EventBridge          | Event routing            |
| AWS Lambda                  | Automated response       |
| AWS Step Functions          | Workflow orchestration   |
| Amazon SNS                  | Alert notification       |
| Amazon Athena               | Security investigation   |
| Amazon CloudWatch Dashboard | Monitoring               |

### 4. Technical Implementation

#### Implementation Phases

- **Phase 1:** Research AWS security services and design the SOC architecture.
- **Phase 2:** Deploy AWS infrastructure using Terraform.
- **Phase 3:** Configure CloudTrail, VPC Flow Logs, GuardDuty, IAM Access Analyzer and Security Hub.
- **Phase 4:** Implement automated response using EventBridge, Lambda, Step Functions and SNS.

#### Technical Requirements

- AWS Security Services
- AWS Networking
- Terraform
- AWS Lambda (Python)
- IAM
- Amazon EventBridge
- AWS Step Functions
- AWS CloudTrail
- Amazon S3
- Amazon Athena
- AWS KMS
- Amazon GuardDuty
- AWS Security Hub
- Amazon CloudWatch

### 5. Timeline & Milestones

- **Month 1**
  - Study AWS security services.
  - Research the NIST Cybersecurity Framework.
  - Design the system architecture.

- **Month 2**
  - Deploy infrastructure.
  - Configure logging.
  - Enable security services.

- **Month 3**
  - Develop automated response.
  - Test detection and response.
  - Complete deployment and documentation.

### 6. Budget Estimation

| Service                     | Estimated Cost           |
| --------------------------- | ------------------------ |
| Amazon S3                   | Low                      |
| Amazon Athena               | Pay per scanned data     |
| Amazon GuardDuty            | Trial / Minimal workload |
| AWS CloudTrail              | Free Management Events   |
| AWS Lambda                  | Free Tier                |
| Amazon EventBridge          | Free Tier                |
| Amazon SNS                  | Free Tier                |
| AWS Security Hub            | Trial / Limited usage    |
| AWS WAF                     | Minimal                  |
| Amazon CloudWatch Dashboard | Minimal                  |
| NAT Instance (t4g.nano)     | Low                      |

**Estimated monthly operating cost:** Under **USD 60**.

### 7. Risk Assessment

#### Risk Matrix

| Risk                       | Impact | Probability |
| -------------------------- | ------ | ----------- |
| False positives            | Medium | Medium      |
| Misconfigured IAM policies | High   | Low         |
| Unexpected AWS costs       | Medium | Low         |
| Lambda execution failures  | Medium | Low         |
| Service quota limitations  | Low    | Low         |

#### Mitigation Strategies

- Configure GuardDuty Suppression Rules.
- Apply least-privilege IAM policies.
- Monitor AWS Budgets.
- Validate automated workflows before deployment.

#### Contingency Plans

- Investigate incidents manually using Athena.
- Restore Security Groups if required.
- Re-enable revoked IAM credentials.
- Roll back infrastructure using Terraform.

### 8. Expected Outcomes

#### Technical Improvements

- Automated cloud threat detection.
- Real-time monitoring.
- Centralized log management.
- Automated incident response.
- Cost-efficient serverless security operations.

#### Long-term Value

The SOC platform serves as a practical reference architecture for learning and implementing cloud security on AWS. It demonstrates how serverless and event-driven AWS services can be integrated to build an automated Security Operations Center following the NIST Cybersecurity Framework. The project can be reused for education, research and future cloud security development.
