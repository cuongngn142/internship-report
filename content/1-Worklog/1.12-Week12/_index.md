---
title: "Week 12 Worklog"
date: 2026-07-06
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Objectives:

* Build a centralized monitoring system.
* Test the complete Security Operations Center architecture.
* Evaluate project results and complete the project documentation.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Build Amazon CloudWatch Dashboard <br> - Display security and operational metrics | 06/07/2026 | 06/07/2026 | https://docs.aws.amazon.com/cloudwatch/ |
| 3 | - Configure CloudWatch Alarms <br> - Test Email Notification through Amazon SNS | 07/07/2026 | 07/07/2026 | https://docs.aws.amazon.com/cloudwatch/ |
| 4 | - Perform simulated attack scenarios <br> - Check Security Findings in GuardDuty and Security Hub | 08/07/2026 | 08/07/2026 | https://docs.aws.amazon.com/guardduty/ |
| 5 | - Evaluate the effectiveness of the Detect → Respond → Recover process <br> - Optimize IAM Policies following the Least Privilege principle | 09/07/2026 | 09/07/2026 | https://docs.aws.amazon.com/iam/ |
| 6 | - Complete deployment documentation <br> - Evaluate costs and propose future system expansion directions | 10/07/2026 | 10/07/2026 | https://docs.aws.amazon.com/wellarchitected/ |

### Week 12 Achievements:

* Successfully built an Amazon CloudWatch Dashboard for centralized monitoring.

* The dashboard displays important metrics including:
  - GuardDuty Findings
  - Security Hub Findings
  - Lambda Invocations
  - Step Functions Executions
  - EC2 Health
  - WAF Blocked Requests
  - CloudFront Requests
  - ALB Request Count

* Configured CloudWatch Alarms and successfully tested email notification delivery through Amazon SNS.

* Performed multiple simulated attack scenarios to evaluate the detection and response capabilities of the system.

* Verified that the complete Detect → Respond → Recover workflow operates correctly according to the designed architecture.

* Optimized IAM Policies following the Least Privilege principle to reduce unnecessary access permissions.

* Evaluated deployment costs and proposed future expansion directions including Multi-AZ, Multi-Account, Infrastructure as Code, Amazon Macie, and Amazon Detective.

* Completed the project report, deployment documentation, and system user guide.