---
title: 'Week 10 Worklog'
date: 2026-06-22
weight: 10
chapter: false
pre: ' <b> 1.10. </b> '
---

---

### Week 10 Objectives:

- Implement an automated incident response system using AWS serverless services.
- Develop Lambda functions to process security findings and perform automatic remediation.
- Integrate Amazon EventBridge to trigger automated response workflows.

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                              | Start Date | Completion Date | Reference Material                          |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------------- |
| 2   | - Create an SNS Topic for security alerts <br> - Subscribe an email endpoint for receiving notifications                                                          | 22/06/2026 | 22/06/2026      | https://docs.aws.amazon.com/sns/            |
| 3   | - Develop Lambda Function #1 to process GuardDuty findings <br> - Parse finding severity and send alerts via SNS                                                  | 23/06/2026 | 23/06/2026      | https://docs.aws.amazon.com/lambda/         |
| 4   | - Develop Lambda Function #2 to automatically block suspicious IP addresses by updating EC2 Security Groups                                                       | 24/06/2026 | 24/06/2026      | https://docs.aws.amazon.com/ec2/            |
| 5   | - Create an EventBridge Rule to trigger Lambda when GuardDuty detects High severity findings <br> - Perform end-to-end testing from GuardDuty to SNS notification | 25/06/2026 | 25/06/2026      | https://docs.aws.amazon.com/eventbridge/    |
| 6   | - Develop Lambda Function #3 to revoke compromised IAM Access Keys automatically <br> - Design an AWS Step Functions workflow for multi-step incident response    | 26/06/2026 | 26/06/2026      | https://docs.aws.amazon.com/step-functions/ |

### Week 10 Achievements:

- Successfully configured Amazon SNS to deliver security notifications via email.

- Developed Lambda functions using Python 3.12 to automatically process GuardDuty findings.

- Implemented automated email notifications based on GuardDuty severity levels.

- Built an automated remediation function to update EC2 Security Groups and block suspicious IP addresses.

- Configured Amazon EventBridge to automatically trigger Lambda functions when GuardDuty detects High severity threats.

- Successfully completed end-to-end testing of the incident response pipeline:
  - GuardDuty Sample Finding
  - EventBridge Rule
  - AWS Lambda
  - Amazon SNS Email Notification

- Implemented automatic IAM Access Key revocation for compromised credentials detected by GuardDuty.

- Designed a Step Functions workflow to orchestrate multi-step incident response processes.

- Followed AWS security best practices by:
  - Using IAM Roles instead of hardcoded credentials
  - Implementing exception handling with try/except
  - Writing execution logs to Amazon CloudWatch Logs
