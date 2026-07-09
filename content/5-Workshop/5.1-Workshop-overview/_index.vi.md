---
title: 'Giới thiệu workshop'
date: 2026-07-09
weight: 2
chapter: false
pre: ' <b> 5.1. </b> '
---

# Giới thiệu

## Giới thiệu về AWS SOC Platform

AWS SOC Platform là một nền tảng Security Operations Center (SOC) trên AWS, được xây dựng nhằm cung cấp khả năng giám sát bảo mật, thu thập log, phát hiện mối đe dọa và tự động phản ứng với các sự kiện bảo mật.

Mục tiêu của workshop là hướng dẫn từng bước triển khai một kiến trúc SOC nhiều lớp (Defense in Depth) trên AWS bằng cách kết hợp các dịch vụ mạng, bảo mật, giám sát và tự động hóa.

## Tổng quan về workshop

- Hạ tầng mạng bảo mật với Amazon VPC.
- Thu thập và lưu trữ log với CloudTrail, VPC Flow Logs và Amazon S3.
- Phát hiện mối đe dọa với GuardDuty, Security Hub và AWS Config.
- Tự động phản ứng với EventBridge, Lambda, Step Functions và SNS.
- Giám sát hệ thống thông qua CloudWatch Dashboard.

Sau khi hoàn thành workshop, bạn sẽ hiểu cách xây dựng một nền tảng SOC có khả năng giám sát, phát hiện và xử lý các sự kiện bảo mật trên AWS.

Sơ đồ dưới đây mô tả kiến trúc AWS SOC Platform được triển khai trong workshop.

![Image](/images/2-Proposal/AWS_SOC_Architecture_final.drawio.png)
