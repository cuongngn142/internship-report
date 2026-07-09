---
title: 'Workshop'
date: 2026-07-09
weight: 1
chapter: false
pre: ' <b> 5. </b> '
---

# Workshop

## Triển khai AWS SOC Platform an toàn và tự động

Workshop này hướng dẫn bạn từng bước thiết kế, cấu hình và triển khai một nền tảng SOC (Security Operations Center) trên AWS. Giải pháp sử dụng các dịch vụ bảo mật, giám sát và tự động hóa của AWS để xây dựng một hệ thống có khả năng thu thập log, phát hiện mối đe dọa, cảnh báo và tự động ứng phó với các sự kiện bảo mật.

Toàn bộ hệ thống được triển khai theo mô hình nhiều lớp bảo mật (Defense in Depth), kết hợp giữa Network Security, Data Collection, Threat Detection, Automated Response và Monitoring Dashboard.

## Architecture Overview

Workshop này bao gồm các lớp chính:

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
   - Kiểm tra luồng hoạt động của hệ thống.
   - Kiểm tra khả năng phát hiện và phản ứng với sự kiện bảo mật.

8. **Resource Cleanup**
   - Xóa các tài nguyên AWS sau khi hoàn thành workshop.

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
