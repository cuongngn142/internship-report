---
title: 'Automated Response'
date: 2026-07-09
weight: 56
chapter: true
pre: '<b>5.6.</b>'
---

# Automated Response

In this chapter, you will build an automated incident response mechanism for the SOC Platform by combining AWS serverless services. When threat detection services generate Security Findings, the platform will automatically trigger response workflows, send notifications, and perform appropriate response actions to minimize incident response time.

After completing this chapter, the platform will be able to automatically receive security events, orchestrate response workflows, and execute response actions without manual intervention.

## Implementation steps

### Create Amazon SNS Topics

- Create SNS Topics for sending security notifications.
- Configure email subscriptions to receive alerts.
- Prepare notification channels for different incident severity levels.

### Create AWS Lambda Functions

- Create Lambda Functions to perform automated response tasks.
- Configure the IAM execution role and environment variables.
- Deploy the function code for notification and incident response operations.

### Create an AWS Step Functions State Machine

- Create a State Machine to orchestrate the response workflow.
- Build a workflow that executes Lambda Functions based on the severity level of security findings.
- Configure the IAM role for AWS Step Functions.

### Create Amazon EventBridge Rules

- Create EventBridge Rules to listen for Security Findings from AWS services.
- Configure event patterns for GuardDuty and Security Hub.
- Connect EventBridge to AWS Step Functions to automatically trigger the response workflow when security incidents are detected.
