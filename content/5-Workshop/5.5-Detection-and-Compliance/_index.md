---
title: 'Detection and Compliance'
date: 2026-07-09
weight: 55
chapter: true
pre: '<b>5.5.</b>'
---

# Detection and Compliance

In this chapter, you will deploy AWS security services to detect threats, monitor resource configurations, and evaluate compliance with security standards. These services collect, analyze, and consolidate security findings from multiple sources to support continuous monitoring and incident response.

After completing this chapter, the SOC Platform will be able to detect suspicious activities, evaluate resource configurations, analyze access permissions, and consolidate security findings into a centralized management dashboard.

## Implementation steps

### Enable Amazon GuardDuty

- Enable Amazon GuardDuty to detect threats in your AWS account.
- Configure protection features such as S3 Protection and Malware Protection.
- Collect and generate Security Findings for monitoring.

### Create an IAM Access Analyzer

- Create an IAM Access Analyzer.
- Analyze IAM policies and resource-based policies.
- Detect resources that may be accessible from outside the AWS account.

### Enable AWS Config

- Enable AWS Config to record the configuration of AWS resources.
- Configure the Delivery Channel and Configuration Recorder.
- Apply AWS Managed Rules to evaluate the compliance of the environment.

### Enable AWS Security Hub

- Enable AWS Security Hub.
- Enable security standards such as AWS Foundational Security Best Practices and CIS AWS Foundations Benchmark.
- Consolidate Security Findings from GuardDuty, AWS Config, and other AWS security services into a unified dashboard.
