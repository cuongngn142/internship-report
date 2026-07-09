---
title: 'Visibility and Dashboard'
date: 2026-07-09
weight: 57
chapter: true
pre: '<b>5.7.</b>'
---

# Visibility and Dashboard

In this chapter, you will build a centralized monitoring system for the SOC Platform using Amazon CloudWatch. Operational metrics, security alerts, and service status will be visualized on a dashboard, while the platform will automatically generate alerts whenever configured thresholds are exceeded.

After completing this chapter, you will have a centralized dashboard to monitor the overall health of the platform and receive timely notifications when incidents or abnormal activities occur.

## Implementation steps

### Create an Amazon CloudWatch Dashboard

- Create a CloudWatch Dashboard to monitor the platform.
- Add widgets to display metrics from GuardDuty, Lambda, Application Load Balancer, Step Functions, and other related services.
- Build a centralized monitoring interface for operating and monitoring the SOC Platform.

### Create Amazon CloudWatch Alarms

- Create CloudWatch Alarms for important metrics.
- Configure alert thresholds for security events and system errors.
- Connect CloudWatch Alarms to Amazon SNS to send notifications when incidents are detected.
