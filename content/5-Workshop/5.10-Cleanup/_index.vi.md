---
title: 'Dọn dẹp tài nguyên'
date: 2026-07-09
weight: 33
chapter: false
pre: ' <b> 5.9. </b> '
---

## Mục tiêu

Sau khi hoàn tất workshop, bạn sẽ dọn dẹp toàn bộ tài nguyên đã tạo để tránh phát sinh chi phí, loại bỏ các dependency còn tồn tại và giữ môi trường AWS sạch sẽ.

## Giải thích dịch vụ

Trong workshop, nhiều dịch vụ AWS có sự phụ thuộc lẫn nhau. Ví dụ:

- CloudFront phải được **Disable** trước khi **Delete**.
- AWS WAF cần gỡ Association trước khi xóa Web ACL.
- NAT Gateway phải chuyển sang trạng thái **Deleted** trước khi có thể giải phóng Elastic IP.
- Một số Security Group hoặc VPC chỉ có thể xóa sau khi các tài nguyên đang sử dụng chúng đã được xóa.

Thực hiện đúng thứ tự sẽ giúp tránh các lỗi dependency và rút ngắn thời gian dọn dẹp.

## Điều kiện tiên quyết

- Đã hoàn thành toàn bộ workshop.
- Đã lưu lại log, hình ảnh hoặc tài liệu cần thiết.
- Đồng ý xóa toàn bộ tài nguyên đã tạo.

![Cleanup overview](/images/5-Workshop/placeholder.svg)

---

## Bước 1. Xóa CloudFront Distribution

1. Mở **Amazon CloudFront Console**.
2. Chọn distribution `soc-platform`.
3. Chọn **Disable**.
4. Chờ trạng thái chuyển thành **Disabled**.
5. Chọn **Delete**.
6. Xác nhận xóa.

![CloudFront cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 2. Xóa AWS WAF Web ACL

1. Mở **AWS WAF Console** tại Region **us-east-1**.
2. Chọn **Web ACLs**.
3. Chọn `soc-platform-web-acl`.
4. Mở tab **Associated AWS resources**.
5. Gỡ toàn bộ Association nếu còn.
6. Mở tab **Logging and metrics**.
7. Chọn **Disable logging**.
8. Quay lại danh sách Web ACL.
9. Chọn **Delete**.

![WAF cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 3. Xóa CloudWatch

### 3.1 Xóa CloudWatch Alarms

1. Mở **Amazon CloudWatch Console**.
2. Chọn **Alarms** → **All alarms**.
3. Chọn các Alarm:

- `soc-platform-guardduty-critical`
- `soc-platform-lambda-errors`
- `soc-platform-waf-high-blocks`

4. Chọn **Actions** → **Delete**.

### 3.2 Xóa Dashboard

1. Chọn **Dashboards**.
2. Chọn `soc-platform-security-dashboard`.
3. Chọn **Delete**.

![CloudWatch cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 4. Xóa EventBridge Rules

1. Mở **Amazon EventBridge Console**.
2. Chọn **Rules**.

Xóa lần lượt:

- `soc-platform-guardduty-findings`
- `soc-platform-securityhub-findings`
- `soc-platform-accessanalyzer-findings`

Đối với mỗi Rule:

1. Mở Rule.
2. Chọn tab **Targets**.
3. Xóa toàn bộ Target.
4. Quay lại danh sách Rules.
5. Chọn **Delete**.

![EventBridge cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 5. Xóa Step Functions

1. Mở **AWS Step Functions Console**.
2. Chọn State Machine `soc-platform-security-response`.
3. Chọn **Delete**.
4. Xác nhận.

![Step Functions cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 6. Xóa Lambda Functions

1. Mở **AWS Lambda Console**.
2. Xóa lần lượt:

- `soc-platform-isolate-ec2`
- `soc-platform-revoke-iam`
- `soc-platform-send-notification`

Đối với mỗi Function:

1. Chọn **Actions**.
2. Chọn **Delete**.

![Lambda cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 7. Xóa SNS Topics

1. Mở **Amazon SNS Console**.
2. Chọn **Topics**.
3. Xóa:

- `soc-platform-critical-alerts`
- `soc-platform-high-alerts`

4. Chọn **Delete** và xác nhận.

![SNS cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 8. Xóa các Security Services

### 8.1 Disable AWS Security Hub

1. Mở **AWS Security Hub Console**.
2. Chọn **Settings** → **General**.
3. Chọn **Disable Security Hub**.
4. Xác nhận.

### 8.2 Disable Amazon GuardDuty

1. Mở **Amazon GuardDuty Console**.
2. Chọn **Settings**.
3. Chọn **Suspend GuardDuty** hoặc **Disable GuardDuty**.
4. Xác nhận.

### 8.3 Xóa IAM Access Analyzer

1. Mở **IAM Console**.
2. Chọn **Access Analyzer**.
3. Chọn `soc-platform-iam-analyzer`.
4. Chọn **Delete**.

### 8.4 Xóa AWS Config

1. Mở **AWS Config Console**.
2. Chọn **Settings**.
3. Chọn **Edit**.
4. Bỏ chọn **Recording is on**.
5. Chọn **Save**.
6. Mở **Rules**.
7. Xóa toàn bộ Config Rules đã tạo.
8. Xóa **Configuration Recorder**.
9. Xóa **Delivery Channel**.

![Security services cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 9. Xóa CloudTrail

1. Mở **AWS CloudTrail Console**.
2. Chọn **Trails**.
3. Chọn `soc-platform-trail`.
4. Chọn **Delete**.
5. Xác nhận.

![CloudTrail cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 10. Xóa VPC Flow Logs

1. Mở **Amazon VPC Console**.
2. Chọn VPC `soc-platform-vpc`.
3. Mở tab **Flow logs**.
4. Chọn Flow Log.
5. Chọn **Actions** → **Delete flow logs**.

![Flow logs cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 11. Xóa Athena và Glue

### 11.1 Xóa Athena Workgroup

1. Mở **Amazon Athena Console**.
2. Chọn **Workgroups**.
3. Chọn `soc-platform-workgroup`.
4. Chọn **Delete**.

### 11.2 Xóa Glue Database

1. Mở **AWS Glue Console**.
2. Chọn **Databases**.
3. Chọn `soc_platform_logs_db`.
4. Chọn **Delete**.

![Athena and Glue cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 12. Xóa Application Load Balancer

1. Mở **Amazon EC2 Console**.
2. Chọn **Load Balancers**.
3. Chọn `soc-platform-alb`.
4. Chọn **Actions** → **Delete load balancer**.
5. Nhập **confirm** để xác nhận.

### Xóa Target Group

1. Chọn **Target Groups**.
2. Chọn `soc-platform-tg`.
3. Chọn **Actions** → **Delete**.

![ALB cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 13. Xóa NAT Gateway và Elastic IP

### 13.1 Xóa NAT Gateway

1. Mở **Amazon VPC Console**.
2. Chọn **NAT Gateways**.
3. Chọn `soc-platform-nat-gw`.
4. Chọn **Delete NAT Gateway**.
5. Chờ trạng thái chuyển thành **Deleted**.

### 13.2 Release Elastic IP

1. Chọn **Elastic IPs**.
2. Chọn Elastic IP có tag `soc-platform-nat-eip`.
3. Chọn **Release Elastic IP addresses**.

![NAT cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 14. Xóa Security Groups

1. Mở **Amazon EC2 Console**.
2. Chọn **Security Groups**.
3. Xóa theo thứ tự:

- `soc-platform-isolation-sg`
- `soc-platform-app-sg`
- `soc-platform-alb-sg`

4. Chọn **Actions** → **Delete security groups**.

> **Lưu ý:** Không thể xóa Default Security Group của VPC.

![Security group cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 15. Xóa các thành phần VPC

### 15.1 Xóa Route Tables

1. Mở **Amazon VPC Console**.
2. Chọn **Route Tables**.
3. Chọn `soc-platform-private-rt`.
4. Mở **Subnet associations**.
5. Hủy Association.
6. Chọn **Delete**.
7. Thực hiện tương tự với `soc-platform-public-rt`.

> **Lưu ý:** Không thể xóa Main Route Table.

### 15.2 Xóa Subnets

1. Chọn **Subnets**.
2. Xóa:

- `soc-platform-public-subnet`
- `soc-platform-private-subnet`

### 15.3 Xóa Internet Gateway

1. Chọn **Internet Gateways**.
2. Chọn `soc-platform-igw`.
3. Chọn **Detach from VPC**.
4. Chọn **Delete Internet Gateway**.

### 15.4 Xóa VPC

1. Chọn **Your VPCs**.
2. Chọn `soc-platform-vpc`.
3. Chọn **Delete VPC**.
4. Nhập **delete** để xác nhận.

![VPC cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 16. Xóa S3 Bucket

> **Lưu ý:** Bucket phải được làm trống trước khi xóa.

1. Mở **Amazon S3 Console**.
2. Chọn bucket `soc-platform-logs-<account-id>`.
3. Chọn **Empty**.
4. Nhập `permanently delete`.
5. Chờ quá trình hoàn tất.
6. Chọn **Delete**.
7. Nhập tên Bucket để xác nhận.

![S3 cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 17. Xóa AWS KMS Key

1. Mở **AWS KMS Console**.
2. Chọn **Customer managed keys**.
3. Chọn Key có Alias `soc-platform-key`.
4. Chọn **Key actions** → **Schedule key deletion**.
5. Chọn thời gian chờ (khuyến nghị tối thiểu **7 ngày**).
6. Chọn **Schedule deletion**.

> **Lưu ý:** AWS KMS Key sẽ không bị xóa ngay mà chỉ được lên lịch xóa.

![KMS cleanup](/images/5-Workshop/placeholder.svg)

---

## Bước 18. Xóa IAM Roles

1. Mở **IAM Console**.
2. Chọn **Roles**.
3. Xóa lần lượt:

- `soc-platform-lambda-execution-role`
- `soc-platform-stepfunctions-role`
- `soc-platform-eventbridge-role`
- `soc-platform-config-role`
- `soc-platform-vpc-flowlogs-role`

4. Với mỗi Role:
   - Chọn **Delete**.
   - Xác nhận.

![IAM cleanup](/images/5-Workshop/placeholder.svg)

---

## Validation

Sau khi hoàn tất, hãy kiểm tra:

- CloudFront Distribution đã được xóa.
- AWS WAF Web ACL không còn tồn tại.
- CloudWatch Dashboard và Alarm đã được xóa.
- EventBridge Rules không còn.
- Step Functions State Machine đã được xóa.
- Lambda Functions đã được xóa.
- SNS Topics đã được xóa.
- GuardDuty và Security Hub đã được Disable.
- AWS Config, CloudTrail và VPC Flow Logs đã được xóa.
- Athena Workgroup và Glue Database không còn.
- Application Load Balancer và Target Group đã được xóa.
- NAT Gateway và Elastic IP đã được giải phóng.
- Security Groups đã được xóa (ngoại trừ Default Security Group).
- VPC cùng các thành phần liên quan đã được xóa.
- S3 Bucket đã được xóa.
- AWS KMS Key đã được lên lịch xóa.
- IAM Roles của workshop đã được xóa.
- AWS Console không còn tài nguyên thuộc workshop `soc-platform`.
