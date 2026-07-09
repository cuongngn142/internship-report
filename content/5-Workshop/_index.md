---
title: 'Workshop'
date: 2026-07-09
weight: 1
chapter: false
pre: ' <b> 5. </b> '
---

# Workshop

## Deploying a Secure and Automated AWS SOC Platform

This workshop guides you step by step through designing, configuring, and deploying a SOC (Security Operations Center) platform on AWS. The solution uses AWS security, monitoring, and automation services to build a platform capable of collecting logs, detecting threats, generating alerts, and automatically responding to security events.

The entire platform is deployed using a Defense in Depth security model, combining multiple security layers including Network Security, Data Collection, Threat Detection, Automated Response, and Monitoring Dashboard.

## Architecture Overview

This workshop includes the following main layers:

1. **Edge Protection**
   - AWS WAF.
   - Amazon CloudFront.
   - WAF Logging.

2. **Network Foundation**
   - Amazon VPC.
   - Public/Private Subnets.
   - Internet Gateway.
   - NAT Gateway.
   - Route Tables.
   - Security Groups.
   - Application Load Balancer.

3. **Data Collection and Storage**
   - AWS KMS.
   - Amazon S3.
   - AWS CloudTrail.
   - VPC Flow Logs.
   - Amazon Athena.
   - AWS Glue Database.

4. **Detection and Compliance**
   - Amazon GuardDuty.
   - IAM Access Analyzer.
   - AWS Config.
   - AWS Security Hub.

5. **Automated Response**
   - Amazon SNS.
   - AWS Lambda.
   - AWS Step Functions.
   - Amazon EventBridge.

6. **Visibility and Dashboard**
   - Amazon CloudWatch Dashboard.
   - CloudWatch Metrics.
   - CloudWatch Alarms.

7. **Test and Validation**
   - Validate the system workflow.
   - Verify the ability to detect and respond to security events.

8. **Resource Cleanup**
   - Remove AWS resources after completing the workshop.

## Content

1. [Workshop Overview](./5.1-Workshop-overview/)
2. [Prerequisites](./5.2-Prerequisites/)
3. [Network & Security Infrastructure](./5.3-Network-foundation/)
4. [Data Collection and Storage](./5.4-Data-Collection-and-Storage/)
5. [Detection and Compliance](./5.5-Detection-and-Compliance/)
6. [Automated Response](./5.6-Automated-Response/)
7. [Visibility and Dashboard](./5.7-Visibility-and-Dashboard/)
8. [Edge Protection](./5.8-Edge-Protection/)
9. [Test & Validation](./5.9-Test-Validation/)
10. [Resource Cleanup](./5.10-Cleanup/)
