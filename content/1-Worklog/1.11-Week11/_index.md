---
title: 'Week 11 Worklog'
date: 2026-06-29
weight: 11
chapter: false
pre: ' <b> 1.11. </b> '
---

### Week 11 Objectives:

- Complete the automated incident response workflow.
- Integrate serverless services into a unified processing workflow.
- Test response scenarios for different types of Security Findings.

### Tasks to be carried out this week:

| Day | Task                                                                                                                           | Start Date | Completion Date | Reference Material                          |
| --- | ------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ------------------------------------------- |
| 2   | - Complete AWS Step Functions to orchestrate the incident response workflow <br> - Connect EventBridge with Step Functions     | 29/06/2026 | 29/06/2026      | https://docs.aws.amazon.com/step-functions/ |
| 3   | - Develop Lambda Function to isolate EC2 using Isolation Security Group <br> - Test the EC2 isolation workflow                 | 30/06/2026 | 30/06/2026      | https://docs.aws.amazon.com/ec2/            |
| 4   | - Develop Lambda Function to disable IAM Access Key <br> - Block IAM User Console login when Credential Compromise is detected | 01/07/2026 | 01/07/2026      | https://docs.aws.amazon.com/iam/            |
| 5   | - Store incident response history in Amazon S3 <br> - Record execution logs in Amazon CloudWatch Logs                          | 02/07/2026 | 02/07/2026      | https://docs.aws.amazon.com/s3/             |
| 6   | - Test the complete Detect → Respond workflow using GuardDuty Sample Findings and Security Hub Findings                        | 03/07/2026 | 03/07/2026      | https://docs.aws.amazon.com/guardduty/      |

### Week 11 Achievements:

- Completed the automated incident response workflow using AWS Step Functions.

- Amazon EventBridge automatically triggers Step Functions when AWS Security Hub generates Security Findings.

- Developed a Lambda Function to automatically isolate EC2 instances through Isolation Security Group.

- Completed the function to automatically disable IAM Access Keys and block IAM User Console access when credential exposure risks are detected.

- Stored incident response history in Amazon S3 for auditing and investigation purposes.

- Recorded all Lambda and Step Functions execution logs in Amazon CloudWatch Logs.

- Successfully tested the automated response workflow from Security Hub → EventBridge → Step Functions → Lambda → SNS.
