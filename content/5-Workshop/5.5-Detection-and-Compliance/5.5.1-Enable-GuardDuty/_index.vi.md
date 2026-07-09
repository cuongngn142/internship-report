---
title: 'Bật GuardDuty'
date: 2026-07-09
weight: 19
chapter: false
pre: ' <b> 5.5.1. </b> '
---

## Mục tiêu

Phát hiện các hoạt động đáng ngờ trên AWS.

## Giải thích dịch vụ

Amazon GuardDuty sử dụng telemetry và machine learning để phát hiện mối đe dọa.

## Bước 1. Mở GuardDuty

- Tìm dịch vụ `GuardDuty`.
- Chọn **Get started**.

![GuardDuty console](/images/5-Workshop/5.5-Detection-Compiance/guardduty.png)

## Bước 2. Bật GuardDuty

- Chọn **Enable GuardDuty**.
  Sau khi enable, click **Settings**:
  - **Finding publishing frequency**: Chọn **15 minutes**
  - **S3 Protection**: Chọn **Enable**
  - **EKS Protection**: Chọn **Enable** (nếu sử dụng EKS)
  - **Malware Protection**: Chọn **Enable**
  - Click **Save**

![GuardDuty form](/images/5-Workshop/5.5-Detection-Compiance/setting-guardduty.png)

## Validation

- GuardDuty đã được bật.
- Các finding bắt đầu được tạo.

![Validation](/images/5-Workshop/5.5-Detection-Compiance/valid-guardduty.png)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo IAM Access Analyzer.
