---
title: 'Proposal'
date: 2026-07-08
weight: 2
chapter: false
pre: ' <b> 2. </b> '
---

---

# Security Operations Center (SOC) on AWS

## Serverless and Event-driven Platform for Automated Security Monitoring, Detection, Response, and Operations

### 1. Executive Summary

In the context of enterprises increasingly adopting cloud computing for infrastructure and application deployment, ensuring information security has become a critical requirement. Although AWS provides numerous security services, security monitoring and incident response processes are often performed separately or manually, resulting in longer detection and response times.

The **Security Operations Center (SOC) on AWS** project is proposed to build a security monitoring and incident response platform based on a **Serverless** and **Event-driven** architecture, enabling automation of log collection, threat detection, incident response, and system monitoring processes.

The solution utilizes AWS services including Amazon CloudTrail, VPC Flow Logs, Amazon GuardDuty, AWS Security Hub, AWS Config, IAM Access Analyzer, Amazon EventBridge, AWS Step Functions, AWS Lambda, Amazon SNS, Amazon CloudWatch, Amazon S3, AWS KMS, and Amazon Athena. When a Security Finding is detected, the system automatically triggers an incident response workflow, performing actions such as isolating EC2 instances, disabling compromised IAM User Access Keys, and sending notifications to administrators.

The architecture is designed based on the **Defense in Depth** security model and aligned with the five functions of the **NIST Cybersecurity Framework**, including **Identify, Protect, Detect, Respond, and Recover**. The project aims to build an automated, easy-to-deploy SOC model suitable for learning, research, and serving as a foundation for developing future cloud security systems on AWS.

---

### 2. Concept & Objectives (Problem Statement)

#### 2.1 Context & Problem

- **System purpose:** The Security Operations Center (SOC) on AWS is developed to build a security monitoring, detection, and incident response platform on AWS using a **Serverless** combined with **Event-driven** architecture. The system automates log collection, threat detection, response orchestration, and notification delivery, reducing incident response time and improving security management efficiency.

- **Target Audience:** The system targets two main groups: **small and medium-sized enterprises (SMEs)** using AWS but without dedicated SOC teams, requiring only **1–2 personnel** to deploy, monitor logs, and handle alerts; and **students, learners, and research groups** who need a practical SOC model for studying, researching, and developing Cloud Security projects.

- **Problem Statement:** AWS security services such as Amazon GuardDuty, AWS Config, and IAM Access Analyzer are capable of detecting threats, evaluating configuration compliance, and identifying unintended resource exposure. AWS Security Hub aggregates, normalizes, and prioritizes Security Findings from these services. However, these services mainly focus on detection and alert generation. Administrators still need to manually review and handle incidents, while security logs are distributed across multiple services, making centralized monitoring difficult.

The project addresses this problem by building a SOC platform that automatically collects logs, detects threats, triggers response workflows, and provides centralized security monitoring in near real time.

---

#### 2.2 Specific Goals

- **Desired Output:**
  The project aims to build a complete Security Operations Center platform with the following main components:

- Design a SOC architecture based on Serverless and Event-driven models.
- Deploy edge protection using Amazon CloudFront, AWS WAF, and AWS Shield Standard.
- Build VPC infrastructure including Public Subnet, Private Subnet, Application Load Balancer, Security Groups, and VPC Flow Logs.
- Centralize logs from CloudTrail, VPC Flow Logs, GuardDuty, AWS Config, and ALB Access Logs into Amazon S3.
- Build threat detection capabilities using GuardDuty, Security Hub, IAM Access Analyzer, and AWS Config.
- Develop automated incident response workflows using EventBridge, Step Functions, and Lambda Functions.
- Configure CloudWatch Dashboard for centralized monitoring.
- Complete deployment documentation using AWS Console and CloudFormation.

- **Success Criteria:**
  The system is considered complete when it satisfies the following criteria:

- Automatically detects Security Findings from Amazon GuardDuty.
- Automatically triggers incident response workflows when security incidents are detected.
- Capable of isolating EC2 instances using an Isolation Security Group.
- Capable of disabling Access Keys and Console Login of compromised IAM Users.
- Sends notifications to administrators through Amazon SNS.
- Stores incident information on Amazon S3 for digital investigation.
- Monitors the entire system through CloudWatch Dashboard and CloudWatch Alarms.
- Encrypts security logs using AWS KMS.
- Implements the Detect → Respond → Recover incident handling process within the overall NIST Cybersecurity Framework functions (**Identify, Protect, Detect, Respond, Recover**).

---

#### 2.3 Program Alignment

The **Security Operations Center (SOC) on AWS** project is aligned with the objectives of the **First Cloud AI Journey (FCAJ)** program by focusing on the practical application of AWS Cloud and Security services to solve real-world cybersecurity problems.

The solution applies AWS services learned during the program, including Amazon EC2, Amazon VPC, IAM, Amazon S3, Amazon CloudTrail, Amazon CloudWatch, Amazon SNS, and AWS Lambda, while extending to advanced security services such as Amazon GuardDuty, AWS Security Hub, AWS Config, IAM Access Analyzer, Amazon EventBridge, AWS Step Functions, AWS WAF, and Amazon CloudFront.

Unlike individual laboratory exercises that focus on separate AWS services, this project integrates these components into a complete Security Operations Center platform capable of automated monitoring, threat detection, and incident response in AWS environments.

The system architecture follows principles from the **AWS Well-Architected Framework**, especially the **Security** and **Operational Excellence** pillars, through the implementation of Defense in Depth, Least Privilege, AWS KMS encryption, centralized logging, and automated response workflows.

The entire system is also aligned with the five functions of the **NIST Cybersecurity Framework**:

| NIST Function | AWS Services                                              |
| ------------- | --------------------------------------------------------- |
| Identify      | IAM Access Analyzer, AWS Config                           |
| Protect       | CloudFront, AWS WAF, AWS Shield Standard, Security Groups |
| Detect        | CloudTrail, VPC Flow Logs, GuardDuty, Security Hub        |
| Respond       | EventBridge, Step Functions, Lambda, SNS                  |
| Recover       | Amazon S3, Amazon Athena                                  |

It should be noted that within the scope of this project, the **Recover** function is mainly represented through centralized incident data storage on Amazon S3 and investigation support using Amazon Athena. This is not a complete system recovery mechanism (such as automated configuration recovery, backup/restore, or disaster recovery failover). These capabilities are considered future expansion directions.

Amazon CloudWatch Dashboard, although appearing in post-incident monitoring workflows, primarily serves the role of **Monitoring/Observability**, supporting system visibility after incidents rather than being a direct component of the Recover function.

Through this project, the implementation process not only strengthens AWS knowledge but also provides practical exposure to modern SOC operations, improving skills in Cloud Security architecture design and automated incident response on AWS.

### 3. Solution Architecture

#### 3.1 Architecture Diagram

![Image](/images/4-EventParticipated/AWS_SOC_Architecture_final.drawio.png)

The **Security Operations Center (SOC) on AWS** system is designed based on a **Serverless** combined with **Event-driven** architecture, where all security events are processed through an asynchronous event processing mechanism.

When a security event or abnormal behavior occurs in the AWS environment, the system automatically collects data, analyzes the impact level, performs appropriate response actions, and sends notifications to administrators without manual intervention.

The architecture is divided into seven main functional layers. Each layer performs a specific role while remaining tightly integrated to create a complete incident response workflow.

---

##### Layer 1 – Edge Protection

This is the first layer responsible for receiving all incoming traffic from the Internet.

Users access applications through **Amazon CloudFront**, which improves content delivery performance, reduces latency, and prevents direct access to the origin server.

At this layer, **AWS WAF** is used to inspect HTTP/HTTPS requests and prevent common attack patterns such as:

- SQL Injection (SQLi)
- Cross-site Scripting (XSS)
- Bot Traffic
- Rate-based Attacks
- IP Reputation List

In parallel, **AWS Shield Standard** provides automatic protection against DDoS attacks at the network and transport layers.

---

##### Layer 2 – Network Infrastructure

After passing through the edge protection layer, traffic enters the Amazon VPC infrastructure.

The network architecture is designed using a separation model between Public and Private Subnets.

The main components include:

- Amazon VPC
- Internet Gateway
- NAT Gateway
- Public Route Table
- Private Route Table
- Application Load Balancer
- Security Groups

The Application Load Balancer receives traffic from CloudFront and distributes requests to EC2 Instances located in the Private Subnet.

Deploying EC2 instances inside a Private Subnet prevents direct Internet access, significantly reducing the attack surface.

---

##### Layer 3 – Data Collection

This layer is responsible for collecting logs and security events generated throughout the system.

Data sources include:

- Amazon CloudTrail
- VPC Flow Logs
- ALB Access Logs
- AWS Config
- GuardDuty Findings
- CloudWatch Logs

CloudTrail records all API calls performed within the AWS account.

VPC Flow Logs capture network traffic information between resources inside the VPC.

AWS Config monitors resource configuration changes.

GuardDuty generates Security Findings when suspicious activities are detected.

By centralizing security data, the system can support digital investigation activities and provide evidence for post-incident analysis.

---

##### Layer 4 – Storage & Analytics

All security-related data is centrally stored in **Amazon S3**.

To ensure data protection, the bucket is configured with:

- Block Public Access
- Versioning
- Server-side Encryption
- AWS KMS Encryption
- Lifecycle Policy

Amazon Athena is used to query log files directly from S3 without requiring database deployment.

This approach reduces storage management costs while enabling efficient log analysis.

---

##### Layer 5 – Threat Detection

This layer is responsible for detecting security threats and aggregating detection results.

The primary services responsible for threat detection and compliance evaluation include:

- Amazon GuardDuty
- AWS Config
- IAM Access Analyzer

Additionally, **AWS Security Hub** does not directly detect threats. Instead, it acts as an aggregator that collects Security Findings from GuardDuty, Config, IAM Access Analyzer, and other security services.

Security Hub normalizes findings into the **AWS Security Finding Format (ASFF)** and assigns severity levels to help administrators prioritize incident handling.

Amazon GuardDuty uses Machine Learning and Threat Intelligence to analyze CloudTrail events, VPC Flow Logs, and DNS Logs, allowing it to detect activities such as:

- Credential Compromise
- Cryptocurrency Mining
- Port Scanning / Reconnaissance
- Suspicious API Calls

Additionally, when enabled, GuardDuty can detect malware activity through extended features such as **GuardDuty Malware Protection for EC2/EBS or S3**. These capabilities are not included in the default GuardDuty configuration.

AWS Config continuously evaluates AWS resources against security compliance rules.

IAM Access Analyzer analyzes resource policies and trust policies to identify unintended external access, such as:

- IAM Roles
- Amazon S3 Buckets
- AWS KMS Keys

---

##### Layer 6 – Automated Response

This is the core component of the SOC system.

When Amazon GuardDuty, AWS Config, or IAM Access Analyzer generates Security Findings, AWS Security Hub aggregates and normalizes these findings.

Amazon EventBridge then receives events from Security Hub and triggers AWS Step Functions.

Step Functions orchestrates the incident response workflow by invoking corresponding Lambda Functions.

Depending on the Security Finding type, Lambda performs response actions such as:

- Isolating EC2 instances using an Isolation Security Group.
- Disabling compromised IAM User Access Keys.
- Blocking IAM User Console Login by deleting Login Profile (DeleteLoginProfile) or applying IAM Deny Policies.
- Sending notifications through Amazon SNS.
- Recording incident handling history into Amazon S3.
- Writing operational logs into CloudWatch Logs.

Through the Event-driven architecture, incident response actions are executed automatically immediately after detection, significantly reducing response time.

---

##### Layer 7 – Monitoring & Visualization

The final layer provides centralized monitoring and system observability.

Amazon CloudWatch Dashboard displays information including:

- Number of Security Findings
- Lambda Invocations
- Lambda Error Rate
- Step Functions Execution
- EC2 Health
- ALB Request Count
- CloudFront Requests
- WAF Blocked Requests
- GuardDuty Findings
- SNS Notifications

CloudWatch Alarms automatically send alerts when monitored metrics exceed configured thresholds.

The dashboard enables administrators to monitor the security status of the entire system in near real time.

---

#### 3.2 Overall Architecture

The system architecture follows the **Defense in Depth** security model, where each layer provides a specific security function to minimize risks and improve threat detection and response capabilities.

The overall system workflow is described as follows:

1. Users send requests from the Internet to Amazon CloudFront.
2. AWS WAF and AWS Shield Standard inspect incoming traffic.
3. Valid traffic is forwarded to the Application Load Balancer.
4. ALB distributes requests to EC2 instances inside the Private Subnet.
5. CloudTrail, VPC Flow Logs, and AWS Config record system activities.
6. Amazon GuardDuty continuously analyzes data from CloudTrail, VPC Flow Logs, and DNS Logs to detect abnormal activities. AWS Config monitors resource configuration changes, while IAM Access Analyzer identifies unintended external resource sharing.
7. AWS Security Hub aggregates Security Findings.
8. Amazon EventBridge receives security events.
9. AWS Step Functions orchestrates the incident response workflow.
10. AWS Lambda performs automated remediation actions.
11. Amazon SNS sends notifications to administrators.
12. All logs and response results are stored in Amazon S3.
13. Amazon Athena supports log querying and investigation.
14. Amazon CloudWatch Dashboard displays system status in real time.

---

#### 3.3 AWS Services Details

| Service                   | Role                                          |
| ------------------------- | --------------------------------------------- |
| Amazon VPC                | Build private network infrastructure          |
| Public & Private Subnet   | Separate public and private access zones      |
| Internet Gateway          | Provide Internet connectivity                 |
| NAT Gateway               | Allow Private Subnet outbound Internet access |
| Application Load Balancer | Load balancing                                |
| Amazon EC2                | Run applications and workloads                |
| Amazon CloudFront         | CDN and edge protection                       |
| AWS WAF                   | Web attack filtering                          |
| AWS Shield Standard       | DDoS protection                               |
| Amazon CloudTrail         | Record API calls                              |
| VPC Flow Logs             | Capture network traffic                       |
| Amazon S3                 | Centralized log storage                       |
| AWS KMS                   | Data encryption                               |
| Amazon Athena             | Log analysis                                  |
| Amazon GuardDuty          | Threat detection                              |
| AWS Security Hub          | Security Finding aggregation                  |
| AWS Config                | Configuration compliance monitoring           |
| IAM Access Analyzer       | Detect unintended resource sharing            |
| Amazon EventBridge        | Event routing and orchestration               |
| AWS Step Functions        | Incident response workflow orchestration      |
| AWS Lambda                | Automated response execution                  |
| Amazon SNS                | Notification delivery                         |
| Amazon CloudWatch         | Monitoring dashboard and alarms               |

### 4. Technical Implementation

#### Implementation Phases

The project is implemented through the following main technical phases:

### Building Network Infrastructure and Edge Protection Layer

Tasks include:

- Creating Amazon VPC.
- Creating Public Subnet and Private Subnet.
- Configuring Internet Gateway and NAT Gateway.
- Setting up Public Route Table and Private Route Table.
- Creating Security Groups based on the **Least Privilege** principle.
- Deploying Application Load Balancer.
- Configuring Amazon CloudFront.
- Deploying AWS WAF and AWS Shield Standard to protect the edge layer.

### Establishing Log Collection and Storage System

Tasks include:

- Enabling Amazon CloudTrail to record API calls.
- Configuring VPC Flow Logs.
- Enabling AWS Config to monitor resource configuration changes.
- Enabling ALB Access Logs.
- Creating Amazon S3 Bucket for centralized log storage.
- Configuring Block Public Access.
- Enabling Versioning.
- Encrypting stored data using AWS KMS.
- Configuring Lifecycle Policy for log data.

### Establishing Threat Detection System

Tasks include:

- Enabling Amazon GuardDuty.
- Enabling AWS Security Hub.
- Configuring AWS Config Rules.
- Creating IAM Access Analyzer.
- Verifying Security Finding aggregation in AWS Security Hub.
- Using GuardDuty Sample Findings and Security Hub Sample Findings for testing purposes.

### Establishing Automated Incident Response Workflow

Tasks include:

- Creating Amazon EventBridge Rule to receive Security Findings from AWS Security Hub.
- Building AWS Step Functions to orchestrate response workflows.
- Developing AWS Lambda Functions to handle different Security Finding types.
- Assigning required IAM Roles and IAM Policies for Lambda.
- Configuring Lambda to isolate EC2 instances using an Isolation Security Group.
- Configuring Lambda to disable compromised IAM Access Keys.
- Configuring Lambda to block IAM User Console Login by deleting Login Profile or applying IAM Deny Policies.
- Sending notifications through Amazon SNS.
- Recording incident response history into Amazon S3.
- Monitoring execution logs through Amazon CloudWatch Logs.

### Establishing Monitoring and Visualization System

Tasks include:

- Building Amazon CloudWatch Dashboard.
- Displaying GuardDuty Findings.
- Displaying Security Hub Findings.
- Monitoring Lambda Invocations and Errors.
- Monitoring Step Functions Executions.
- Monitoring EC2 Health.
- Monitoring CloudFront Requests.
- Monitoring ALB Request Count.
- Monitoring WAF Blocked Requests.
- Configuring CloudWatch Alarms.
- Testing email notifications through Amazon SNS.

### System Testing

Testing activities include:

- Simulating Port Scan activities on EC2.
- Simulating Credential Compromise scenarios.
- Simulating Security Group exposure of SSH access to the Internet.
- Simulating Public S3 Bucket exposure.
- Verifying GuardDuty Security Finding generation.
- Verifying Security Hub Finding aggregation.
- Verifying EventBridge triggering AWS Step Functions.
- Verifying AWS Lambda automated response execution.
- Verifying Email Notifications.
- Verifying CloudWatch Dashboard and CloudWatch Alarms.

### System Optimization and Completion

Tasks include:

- Validating the complete **Detect → Respond → Recover** workflow.
- Optimizing IAM Policies based on the Least Privilege principle.
- Evaluating deployment costs using AWS Pricing Calculator.
- Completing deployment documentation.
- Preparing future expansion directions such as Multi-AZ, Multi-Account, and Infrastructure as Code.

#### Prerequisites

- **Required Resources and Tools:** AWS Account with permissions to use Amazon EC2, Amazon VPC, IAM, Amazon CloudTrail, Amazon GuardDuty, AWS Security Hub, AWS Config, IAM Access Analyzer, Amazon EventBridge, AWS Step Functions, AWS Lambda, Amazon SNS, Amazon CloudWatch, Amazon S3, AWS KMS, Amazon Athena, AWS WAF, and Amazon CloudFront.
- Web browser for accessing AWS Management Console.
- Computer with stable Internet connection.
- Email address for receiving notifications from Amazon SNS.
- **Required Knowledge:**
  The following knowledge areas are required:

- Amazon VPC, Subnet, Route Table, Internet Gateway, and NAT Gateway.
- Security Groups and the **Least Privilege** principle.
- Amazon EC2 and IAM Roles.
- Amazon CloudTrail and VPC Flow Logs.
- AWS Config and IAM Access Analyzer.
- Amazon GuardDuty and AWS Security Hub.
- Amazon EventBridge.
- AWS Step Functions.
- AWS Lambda.
- Amazon SNS.
- Amazon CloudWatch Dashboard and CloudWatch Alarms.
- Amazon S3, AWS KMS, and Amazon Athena.
- Basic knowledge of Cloud Security, Incident Response, and the **NIST Cybersecurity Framework**.

---

### 5. Timeline & Milestones

- **Week 1: Security Monitoring and Threat Detection Setup**
- Create AWS Account and configure basic security settings (enable MFA for Root User, create IAM User with administrative permissions).
- Enable Amazon CloudTrail to record API Calls.
- Configure VPC Flow Logs for network traffic collection.
- Enable AWS Config to monitor resource configuration changes.
- Create AWS Budgets and cost alerts.
- Enable Amazon GuardDuty.
- Enable AWS Security Hub and integrate GuardDuty Findings.
- Create IAM Access Analyzer to identify unintended resource exposure.
- Configure CloudWatch Alarms for important events.
- Generate GuardDuty Sample Findings and verify Security Hub Finding aggregation.
- **Week 2: Automated Incident Response Development**
- Create Amazon SNS Topic and Email Subscription for notifications.
- Develop AWS Lambda Functions for Security Finding processing.
- Build Lambda function to automatically isolate EC2 instances using Isolation Security Group.
- Build Lambda function to automatically disable compromised IAM Access Keys.
- Create Amazon EventBridge Rule to receive Security Findings from AWS Security Hub.
- Design incident response workflow using AWS Step Functions.
- Integrate EventBridge, Step Functions, and Lambda into an automated response process.
- Test the workflow:
  **GuardDuty → Security Hub → EventBridge → Step Functions → Lambda → SNS**
- Store execution logs in Amazon CloudWatch Logs.
- **Week 3: Incident Response Completion and Data Storage**
- Complete Lambda Functions for different Security Finding scenarios.
- Configure IAM Roles and IAM Policies following the Least Privilege principle.
- Implement IAM User Console Login blocking when Credential Compromise is detected.
- Store incident history and response results in Amazon S3.
- Encrypt stored data using AWS KMS.
- Perform testing scenarios:
  - EC2 Port Scan.
  - Credential Compromise.
  - Security Group exposing SSH to the Internet.
  - Public S3 Bucket.
- Evaluate detection capability and incident response time.
  - **Week 4: Monitoring, Testing, and System Completion**
- Build Amazon CloudWatch Dashboard for centralized monitoring.
- Display GuardDuty Findings, Security Hub Findings, and AWS Config Compliance status.
- Monitor Lambda Invocations, Lambda Errors, and Step Functions Executions.
- Monitor EC2 Health, CloudFront Requests, ALB Request Count, and WAF Blocked Requests.
- Configure CloudWatch Alarms and test email notifications through Amazon SNS.
- Validate the complete Detect → Respond → Recover workflow.
- Evaluate deployment cost using AWS Pricing Calculator.
- Complete deployment documentation and user guide.
- Evaluate achieved results and propose future expansion directions including Multi-AZ, Multi-Account, Infrastructure as Code (Terraform/CloudFormation), Amazon Macie, Amazon Detective, and SIEM integration.

---

### 6. Budget Estimation

The detailed cost estimation of the system is based on the [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=e3157d6bc8f89ac9ba160192d26e64ca7d3c0cde)

#### 6.1 Workshop / Testing Environment

The Workshop environment is designed for learning, research, and demonstrating the detection, analysis, and incident response capabilities of the SOC system.

The environment uses several AWS services similar to a real-world deployment, including ALB, NAT Gateway, WAF, GuardDuty, AWS Config, and Security Hub, but with limited resource scale and low traffic volume.

| No.                         | AWS Service               | Configuration & Calculation Parameters                 |      Monthly Cost |
| --------------------------- | ------------------------- | ------------------------------------------------------ | ----------------: |
| 1                           | Amazon EC2                | 01 t3.micro Linux instance, On-Demand, 730 hours/month |             $9.64 |
| 2                           | Application Load Balancer | 01 ALB, low traffic                                    |            $18.63 |
| 3                           | NAT Gateway               | 01 NAT Gateway running continuously                    |            $43.66 |
| 4                           | Amazon S3                 | 20 GB Standard Storage, PUT/GET requests               |             $0.79 |
| 5                           | Amazon CloudFront         | 10 GB Data Transfer Out, 500,000 HTTPS requests        |             $1.35 |
| 6                           | Amazon API Gateway        | Small-scale HTTP/REST API requests                     |             $1.25 |
| 7                           | Amazon CloudWatch         | 5 GB Logs, 20 Metrics, 1 Dashboard, 10 Alarms          |            $15.80 |
| 8                           | Amazon EBS                | 30 GB gp3 SSD, Snapshot                                |             $8.87 |
| 9                           | AWS KMS                   | 01 Customer Managed Key, 10,000 requests               |             $1.03 |
| 10                          | Amazon CloudTrail         | Management Events, 01 Trail                            |             $0.00 |
| 11                          | Amazon GuardDuty          | CloudTrail Events, VPC Flow Logs, DNS Logs             |            $11.96 |
| 12                          | AWS Config                | 5,000 Configuration Items, 10 Rules                    |            $15.01 |
| 13                          | AWS Security Hub          | Security Checks and Findings                           |             $0.00 |
| 14                          | Amazon Athena             | Querying logs on S3                                    |             $0.00 |
| 15                          | AWS Lambda                | 50,000 requests/month                                  |             $0.00 |
| 16                          | Amazon EventBridge        | 100,000 events/month                                   |             $0.00 |
| 17                          | Amazon SNS                | Email notifications                                    |             $0.00 |
| 18                          | AWS WAF                   | 01 Web ACL, 10 Rules                                   |            $15.60 |
| 19                          | AWS Step Functions        | Standard Workflow, 20,000 state transitions/month      |             $0.40 |
| **Estimated Monthly Total** |                           |                                                        | **$144.00/month** |

---

_Note:_ The above cost assumes all services run continuously. In a learning environment, costs can be significantly reduced by:

- Stopping EC2 instances when not in use.
- Removing NAT Gateway after demonstrations because it has a fixed hourly cost.
- Reducing CloudWatch Logs and S3 log retention periods.
- Reducing the number of AWS Config Rules.
- Using AWS Free Tier, AWS Credits, or educational support programs.

#### 6.2 Production Deployment (SaaS Model)

When deployed in a production environment, the SOC system requires additional resources to meet requirements for performance, high availability, long-term log storage, and continuous security monitoring.

Based on the current Workshop/Demonstration environment cost (~$144.00/month), the Production environment requires additional resources such as more EC2 instances, Multi-AZ deployment, increased log storage capacity, higher Security Finding volume, and expanded analytics capabilities.

The following Production cost estimation is for reference only:

| No.                         | Component                 | Configuration & Calculation Parameters        |        Monthly Cost |
| --------------------------- | ------------------------- | --------------------------------------------- | ------------------: |
| 1                           | Amazon EC2                | 02–04 EC2 instances (t3.medium or equivalent) |        ~$120 - $250 |
| 2                           | Amazon EBS                | 100–200 GB gp3 SSD                            |          ~$10 - $20 |
| 3                           | Application Load Balancer | 01 Production ALB with higher traffic volume  |          ~$25 - $50 |
| 4                           | NAT Gateway               | Multi-AZ NAT Gateway deployment               |         ~$70 - $100 |
| 5                           | Amazon S3                 | 200 GB – 1 TB log storage                     |          ~$10 - $30 |
| 6                           | AWS KMS                   | Customer Managed Keys and encryption requests |            ~$2 - $5 |
| 7                           | Amazon CloudTrail         | Continuous audit logging                      |           ~$5 - $20 |
| 8                           | VPC Flow Logs             | Production network traffic logging            |          ~$10 - $50 |
| 9                           | Amazon GuardDuty          | Continuous threat detection                   |         ~$20 - $100 |
| 10                          | AWS Config                | Multiple Configuration Items and Rules        |         ~$20 - $100 |
| 11                          | IAM Access Analyzer       | Account Analyzer                              |               $0.00 |
| 12                          | AWS Security Hub          | Security Checks and Findings                  |          ~$10 - $50 |
| 13                          | Amazon Athena             | Frequent log queries                          |         ~$20 - $100 |
| 14                          | AWS Lambda                | Automated Response Functions                  |           ~$5 - $20 |
| 15                          | Amazon EventBridge        | Event Processing                              |           ~$5 - $20 |
| 16                          | AWS Step Functions        | Incident Response Workflow                    |           ~$5 - $30 |
| 17                          | Amazon SNS                | Notification Service                          |           ~$1 - $10 |
| 18                          | Amazon CloudWatch         | Logs, Metrics, Dashboard, Alarms              |         ~$30 - $100 |
| 19                          | AWS WAF                   | Web ACL, Managed Rules, Request Processing    |         ~$20 - $100 |
| 20                          | AWS Shield Standard       | Basic DDoS Protection                         |               $0.00 |
| 21                          | Amazon CloudFront         | CDN and Internet Traffic Processing           |          ~$10 - $50 |
| **Estimated Monthly Total** |                           |                                               | **$200~$800/month** |

_Note:_ Production costs cannot be accurately determined only from the number of services. Actual costs depend on:

- Number of applications and resources requiring protection.
- Internet traffic volume.
- Amount of logs generated daily.
- Log retention period required for incident investigation.
- Number of Security Findings generated by GuardDuty and Security Hub.
- Execution frequency of Lambda, Step Functions, and EventBridge.
- High Availability (Multi-AZ) and Disaster Recovery requirements.

---

### 7. Risk Assessment

#### Risk Matrix

During the deployment of the Security Operations Center (SOC) on AWS, several risks may affect the system's monitoring, detection, and incident response capabilities.

The risks are evaluated based on two main factors: probability of occurrence and impact level on the system.

| Identified Risk                                                                                          | Likelihood | Impact    | Mitigation and Prevention Strategy                                                                                                                                           |
| -------------------------------------------------------------------------------------------------------- | ---------- | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IAM Roles or IAM Policies provide excessive permissions to Lambda and automated services                 | Medium     | High      | Apply the Least Privilege principle. Grant only required permissions to each Lambda Function. Use IAM Access Analyzer to review unintended access.                           |
| EC2 instances are accessed without authorization or exploited through vulnerabilities                    | Medium     | High      | Place EC2 instances in Private Subnet, avoid direct SSH exposure from the Internet, restrict Security Groups, apply security patches regularly, and monitor using GuardDuty. |
| Security Findings are not detected due to incorrect GuardDuty, Security Hub, or CloudTrail configuration | Low        | High      | Verify that security services are enabled correctly. Use GuardDuty Sample Findings and Security Hub Sample Findings for periodic testing.                                    |
| Lambda performs incorrect response actions affecting legitimate resources                                | Medium     | High      | Test workflows before production deployment, use Step Functions for workflow control, maintain detailed CloudWatch logs, and implement rollback mechanisms.                  |
| EventBridge fails to trigger response workflows when Security Findings occur                             | Low        | High      | Verify Event Pattern configuration, service permissions, Step Functions execution status, and create CloudWatch Alarms for EventBridge/Lambda failures.                      |
| Loss or modification of logs used for incident investigation                                             | Low        | High      | Store logs centrally in Amazon S3, enable Versioning, encrypt using AWS KMS, enable Block Public Access, and apply Lifecycle Policy.                                         |
| AWS costs exceed the expected budget                                                                     | Medium     | Medium    | Configure AWS Budget and Cost Alerts, monitor Cost Explorer, limit test resources, and remove expensive fixed-cost services such as NAT Gateway when unnecessary.            |
| NAT Gateway, ALB, or CloudWatch Logs generate high costs in demonstration environments                   | High       | Medium    | Maintain resources only during demonstrations, reduce log volume, apply S3 Lifecycle Policy, and validate costs using AWS Pricing Calculator before deployment.              |
| Security Hub or GuardDuty generates too many Findings, making incident handling difficult                | Medium     | Medium    | Prioritize Findings by severity level, filter important events, and configure EventBridge Rules to process only critical security events.                                    |
| Incorrect AWS Config Rules result in inaccurate compliance evaluation                                    | Medium     | Medium    | Review Config Rules before deployment, use appropriate AWS Managed Rules, and monitor compliance status regularly.                                                           |
| AWS Account loses control or credentials are compromised                                                 | Low        | Very High | Enable MFA for Root Account, avoid regular Root User usage, use dedicated IAM Users/Roles, and monitor activities through CloudTrail.                                        |
| Automated response system fails during security incidents                                                | Low        | High      | Maintain manual response procedures, keep administrative access available, and regularly test the complete Detect → Respond workflow.                                        |

#### Contingency Plan

- **Case 1: Security Finding Detected but Automated Response Fails** When GuardDuty or Security Hub detects an incident but EventBridge, Step Functions, or Lambda cannot execute the response action, administrators should check:

- AWS CloudWatch Logs of Lambda Functions.
- AWS Step Functions execution status.
- EventBridge Rules and permissions between AWS services.

If necessary, administrators can perform manual response actions such as:

- Isolating EC2 instances by modifying Security Groups.
- Disabling suspicious IAM Access Keys.
- Adjusting IAM Policies to restrict access.

- **Case 2: EC2 Instance Is Compromised or Shows Abnormal Behavior:** When GuardDuty detects activities such as Port Scanning, Credential Compromise, or suspicious behavior:

The response workflow is:

1. GuardDuty generates a Security Finding.
2. Security Hub aggregates and normalizes the Finding.
3. EventBridge triggers the response workflow.
4. Lambda isolates the EC2 instance using an Isolation Security Group.
5. SNS sends notifications to administrators.
6. Incident logs are stored in Amazon S3 for investigation.

If automated response fails, administrators perform manual isolation through AWS Console.

- **Case 3: Log Data Loss or Query Failure:** If Amazon S3, CloudTrail, or Athena experiences issues:

Actions:

- Verify CloudTrail, VPC Flow Logs, and AWS Config logging status.
- Check IAM permissions for S3 Bucket access.
- Restore data from S3 Versioning if logs are unintentionally modified.
- Use CloudWatch Logs as a temporary investigation source.

- **Case 4: Lambda Processes Security Findings Incorrectly:** If Lambda performs incorrect actions on valid resources:

Actions:

- Disable or stop the EventBridge Rule triggering the workflow.
- Review CloudWatch Logs to identify the root cause.
- Restore Security Groups or IAM Policies to previous states.
- Update response logic before re-enabling automation.

- **Case 5: AWS Costs Exceed Expected Budget:** Because the Workshop environment uses several fixed-cost services such as Application Load Balancer, NAT Gateway, AWS Config, and WAF, costs may increase when resources are continuously running.

Mitigation actions:

- Use AWS Cost Explorer to identify cost sources.
- Stop EC2 instances when not required.
- Remove NAT Gateway, ALB, or WAF after demonstrations.
- Reduce CloudWatch Logs and S3 log retention periods.
- Configure AWS Budget Alerts before exceeding the planned budget.

- **Case 6: Requirement to Restore the Entire System:** For Production environments, possible expansion approaches include:

- Using Infrastructure as Code with Terraform or CloudFormation to recreate the environment.
- Backing up IAM configurations, Security Groups, and critical resources.
- Deploying Multi-AZ architecture for higher availability.
- Using S3 Versioning and backup strategies to protect security log data.

The system is designed to prioritize early detection, automated response, and manual recovery procedures when automated components fail, ensuring that SOC monitoring and incident handling capabilities remain available.

### 8. System Processing Flows & Technical Characteristics

The **Security Operations Center (SOC) on AWS** system is built using a **Serverless combined with Event-driven architecture**, where security events are collected, analyzed, processed, and automatically responded to through a chain of AWS services.

The main processing flows include: application access flow, security data collection flow, threat detection flow, automated response flow, administrator notification flow, and incident investigation storage flow.

#### 8.1 Core Processing Flows

- **User Application Access Flow:**
  Users access the system through **Amazon CloudFront**.

All HTTP/HTTPS traffic is first inspected by **AWS WAF** to detect and prevent common attacks such as SQL Injection, Cross-site Scripting (XSS), Bot Traffic, or abnormal requests.

Additionally, **AWS Shield Standard** provides automatic protection against DDoS attacks at the network and transport layers.

After passing through the edge protection layer, valid traffic is forwarded to the **Application Load Balancer**, which distributes requests to EC2 Instances located in the Private Subnet.

Placing EC2 instances inside a Private Subnet reduces direct Internet exposure and minimizes the attack surface.

- **Secure Administration Flow:**
  Administrators do not directly access resources through unnecessary public access points.

System administration is performed through AWS security mechanisms such as:

- IAM Roles with minimum required permissions (Least Privilege).
- MFA for administrator accounts.
- Restricted Security Groups.
- AWS Systems Manager Session Manager (when required for EC2 administration).

This approach reduces risks related to brute-force attacks, credential leakage, and long-term credential usage.

- **Security Data Collection Flow:**
  The system collects security data from multiple sources across the AWS environment:

- **Amazon CloudTrail:** Records API Calls and administrative activities.
- **VPC Flow Logs:** Records network traffic between VPC resources.
- **AWS Config:** Tracks resource configuration changes and evaluates compliance.
- **ALB Access Logs:** Records application access requests.
- **CloudWatch Logs:** Stores operational logs from AWS services.

All log data is centrally stored in **Amazon S3** and encrypted using **AWS KMS** to ensure data confidentiality and support post-incident investigation.

- **Threat Detection Flow:**
  **Amazon GuardDuty** continuously analyzes data from CloudTrail, VPC Flow Logs, and DNS Logs to detect suspicious activities.

Detected activities include:

- Port Scanning.
- Credential Compromise.
- Suspicious API Calls.
- Unusual Network Activity.
- Malware Activity (when appropriate additional protection features are enabled).

Additionally:

- **AWS Config** detects security configuration violations.
- **IAM Access Analyzer** identifies unintended external resource access.

After detection, Security Findings are sent to **AWS Security Hub** for aggregation, normalization, and severity evaluation.

- **Automated Incident Response Flow:**
  When AWS Security Hub generates a Security Finding, the automated response workflow is triggered:

**Security Hub → EventBridge → Step Functions → Lambda → SNS**

Detailed process:

1. **Amazon EventBridge** receives Security Findings from AWS Security Hub.
2. EventBridge Rules evaluate event type and severity level.
3. **AWS Step Functions** orchestrates the response workflow.
4. **AWS Lambda** performs corresponding remediation actions.

Response actions may include:

- Isolating EC2 instances using Isolation Security Groups.
- Disabling compromised IAM Access Keys.
- Applying IAM Deny Policies to restrict access.
- Recording incident response history.
- Sending notifications to administrators.

Execution results are recorded in **Amazon CloudWatch Logs** for auditing and troubleshooting.

- **Administrator Notification Flow:**
  After the response process completes, **Amazon SNS** sends notifications to administrators.

Notification contents include:

- Security Finding type.
- Severity level.
- Detection timestamp.
- Affected resources.
- Response actions performed.

This enables administrators to quickly understand system status and perform additional actions if required.

- **Incident Storage and Investigation Flow:**
  All incident-related information is stored in **Amazon S3**.

Administrators can use **Amazon Athena** to directly query log data stored in S3 for:

- Investigating incident origins.
- Analyzing attack behaviors.
- Tracking activities of AWS accounts or resources.

This mechanism supports Digital Forensics activities after security incidents.

#### 8.2 Architectural Strengths

- **Defense in Depth Security Model:**
  The system does not rely on a single security mechanism but combines multiple protection layers:

- CloudFront.
- AWS WAF.
- AWS Shield Standard.
- VPC Security Groups.
- IAM.
- CloudTrail.
- GuardDuty.
- Security Hub.
- Lambda Response.

Each layer provides a dedicated security function, reducing the possibility of successful exploitation when one protection layer fails.

- **Centralized Data Collection and Monitoring:**
  Instead of managing distributed logs across multiple services, the system centralizes security data in Amazon S3.

Benefits include:

- Easier data searching.
- Support for incident investigation.
- Long-term log retention.
- Reduced operational complexity.

- **TAutomated Incident Response:**
  The combination of Security Hub, EventBridge, Step Functions, and Lambda creates a lightweight SOAR (Security Orchestration, Automation, and Response) model.

The system not only detects security issues but also automatically performs response actions, reducing incident handling time.

- **Least Privilege Implementation:**
  Services in the system receive permissions through IAM Roles with minimum required privileges.

IAM Access Analyzer helps identify unintended permissions and reduces the risk of excessive access or data exposure.

- **High Scalability:**
  The Event-driven architecture enables easy expansion:

- Adding new security data sources.
- Adding new response workflows.
- Integrating SIEM platforms.
- Applying AI-based Security Finding analysis.

- **Easy Testing Capability:**
  AWS provides features such as GuardDuty Sample Findings and Security Hub Sample Findings to simulate security incidents.

This allows validation of the complete workflow:
**Detect → Respond → Recover**
without waiting for real attacks to occur.

---

### 9. Expected Outcomes

- **Technical Improvements:**
  Successfully build a Security Operations Center (SOC) model on AWS using a Serverless combined with Event-driven architecture, capable of automatically collecting logs, detecting threats, orchestrating incident response workflows, and sending real-time alerts. The system supports centralized log storage on Amazon S3, analysis through Amazon Athena, and monitoring through Amazon CloudWatch Dashboard.

- **Long-Term Value:**
  Establish a modern Cloud Security architecture applying Defense in Depth, Least Privilege, and Automated Incident Response principles. The system can be expanded toward Multi-Account, Multi-Region architectures, integrated with additional AWS security services or SIEM platforms, and serves as a reference model for learning, research, and practical SOC deployment.
