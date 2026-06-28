---
title: 'Week 9 Worklog'
date: 2026-06-15
weight: 9
chapter: false
pre: ' <b> 1.9. </b> '
---

### Week 9 Objectives:

- Build the basic AWS security monitoring environment.
- Configure logging, monitoring, and security services for continuous visibility and threat detection.

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                             | Start Date | Completion Date | Reference Material                       |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ---------------------------------------- |
| 2   | - Create AWS account and enable MFA for the root user <br> - Create an IAM Administrator user for daily operations                                                               | 15/06/2026 | 15/06/2026      | https://docs.aws.amazon.com/iam/         |
| 3   | - Enable AWS CloudTrail to record API activities <br> - Configure VPC Flow Logs and send logs to CloudWatch Logs                                                                 | 16/06/2026 | 16/06/2026      | https://docs.aws.amazon.com/cloudtrail/  |
| 4   | - Enable AWS Config to record configuration changes <br> - Configure AWS Budgets with a monthly cost alert                                                                       | 17/06/2026 | 17/06/2026      | https://docs.aws.amazon.com/config/      |
| 5   | - Enable Amazon GuardDuty in ap-southeast-1 <br> - Enable AWS Security Hub with the NIST 800-53 standard <br> - Integrate GuardDuty findings into Security Hub                   | 18/06/2026 | 18/06/2026      | https://docs.aws.amazon.com/securityhub/ |
| 6   | - Enable IAM Access Analyzer <br> - Create CloudWatch alarms for failed login and root account usage <br> - Generate GuardDuty sample findings and verify alerts in Security Hub | 19/06/2026 | 19/06/2026      | https://docs.aws.amazon.com/guardduty/   |

### Week 9 Achievements:

- Successfully configured IAM security best practices by enabling MFA for the root account and using an IAM Administrator user for daily administration.

- Enabled AWS CloudTrail to record all API calls across the AWS account.

- Configured VPC Flow Logs to collect network traffic logs and send them to Amazon CloudWatch Logs.

- Enabled AWS Config to continuously monitor and record resource configuration changes.

- Created an AWS Budget with monthly cost alerts to help control AWS spending.

- Enabled Amazon GuardDuty to detect suspicious activities and potential security threats.

- Enabled AWS Security Hub and integrated GuardDuty findings into a centralized security dashboard.

- Configured IAM Access Analyzer to detect resources shared with external accounts.

- Created CloudWatch alarms for important security events such as failed login attempts and root account usage.

- Successfully generated GuardDuty sample findings and verified that security findings were correctly displayed in AWS Security Hub.
