---
title: 'Kiểm thử & Xác thực'
date: 2026-07-09
weight: 59
chapter: false
pre: ' 5.9. '
---

# Kiểm thử & Xác thực (Test & Validation)

Trong bài lab này, chúng ta sẽ thực hiện end-to-end các bước kiểm thử theo đúng luồng người dùng và luồng hệ thống nhằm đảm bảo toàn bộ kiến trúc SOC Automation hoạt động chính xác, từ lúc Security Hub phát hiện cảnh báo cho đến khi AWS Step Functions điều phối workflow, Lambda xử lý phản ứng và Amazon SNS gửi thông báo đến quản trị viên.

---

# 1. Kiểm thử phản ứng Critical - Isolate EC2

## Kịch bản

Đây là phản ứng mạnh mẽ nhất của hệ thống.

Khi Security Hub phát hiện EC2 Instance có dấu hiệu bị nhiễm malware hoặc thực hiện hành vi bất thường (ví dụ Bitcoin Mining, Command & Control, Data Exfiltration...), workflow sẽ ưu tiên cô lập (Isolation) EC2 ngay lập tức để ngăn chặn việc lây lan hoặc tiếp tục khai thác trong hệ thống.

---

## Bước 1: Mở Step Functions

Truy cập

**AWS Console → Step Functions → State machines → SecurityAutomationWorkflow**

Chọn **Start execution**.

![Image](/images/5-Workshop/5.9-Test-Validation/5.9-Test-Validation/anh1.png)

---

## Bước 2: Dán Event JSON

Sử dụng dữ liệu sau:

```json
{
  "version": "0",
  "id": "12345678-1234-1234-1234-123456789012",
  "detail-type": "Security Hub Findings - Imported",
  "source": "aws.securityhub",
  "account": "629068383761",
  "time": "2026-07-09T13:35:00Z",
  "region": "ap-southeast-1",
  "resources": [],
  "detail": {
    "findings": [
      {
        "SchemaVersion": "2018-10-08",
        "Id": "arn:aws:securityhub:ap-southeast-1:<Điền AWS ACCOUNT ID>:finding/critical-ec2-malware-example",
        "ProductArn": "arn:aws:securityhub:ap-southeast-1::product/aws/guardduty",
        "GeneratorId": "aws-guardduty",
        "AwsAccountId": "<Điền AWS ACCOUNT ID>",
        "Types": ["Effects/Data Exfiltration"],
        "FirstObservedAt": "2026-07-09T13:30:00.000Z",
        "LastObservedAt": "2026-07-09T13:32:00.000Z",
        "CreatedAt": "2026-07-09T13:30:00.000Z",
        "UpdatedAt": "2026-07-09T13:32:00.000Z",
        "Severity": {
          "Product": 8,
          "Normalized": 80,
          "Label": "HIGH"
        },
        "Title": "CryptoCurrency:EC2/BitcoinTool.B",
        "Description": "EC2 instance is querying malware domains associated with Bitcoin mining.",
        "Resources": [
          {
            "Type": "AwsEc2Instance",
            "Id": "<Điền AWS EC2 ID>",
            "Region": "ap-southeast-1"
          }
        ],
        "WorkflowState": "NEW",
        "RecordState": "ACTIVE"
      }
    ]
  }
}
```

![Image](/images/5-Workshop/5.9-Test-Validation/5.9-Test-Validation/anh2.png)

---

## Bước 3: Theo dõi Execution

Quan sát workflow thực thi.

Đường đi mong đợi:

```
Parse Finding
        ↓
Check Severity
        ↓
Isolate EC2
        ↓
Send Notification
```

![Image](/images/5-Workshop/5.9-Test-Validation/5.9-Test-Validation/anh3.png)

Hình ảnh trước khi EC2 bị cô lập bằng cách đổi security group sang một sg với không outbound và inbound

![Image](/images/5-Workshop/5.9-Test-Validation/5.9-Test-Validation/anh6.png)

Hình ảnh sau khi EC2 bị cô lập

![Image](/images/5-Workshop/5.9-Test-Validation/5.9-Test-Validation/anh7.png)

---

## Bước 4: Kiểm tra CloudWatch Logs

Truy cập:

```
CloudWatch
→ Log Groups
→ /aws/lambda/dev-isolate-ec2
```

Kiểm tra log Lambda đã thực hiện thao tác cô lập EC2.

![Image](/images/5-Workshop/5.9-Test-Validation/5.9-Test-Validation/anh4.png)

---

## Bước 5: Kiểm tra Email

Mở Email đã đăng ký SNS.

Kiểm tra nội dung cảnh báo EC2 đã bị cô lập.

![Image](/images/5-Workshop/5.9-Test-Validation/5.9-Test-Validation/anh5.png)

---

## Kết quả mong đợi

- Step Function hoàn thành thành công.
- Lambda Isolate EC2 được gọi.
- CloudWatch ghi log đầy đủ.
- Email cảnh báo được gửi.
- EC2 được chuyển sang Security Group Isolation.

---

# 2. Kiểm thử phản ứng Critical - Revoke IAM Access Key

## Kịch bản

Khi phát hiện IAM Access Key bị lộ hoặc bị công khai, hệ thống ưu tiên bảo vệ tài khoản bằng cách thu hồi Access Key ngay lập tức nhằm ngăn chặn việc sử dụng trái phép.

---

## Bước 1: Mở Step Functions

Lặp lại các bước của phần 1.

---

## Bước 2: Dán Event JSON

```json
{
  "version": "0",
  "id": "22222222-2222-2222-2222-222222222222",
  "detail-type": "Security Hub Findings - Imported",
  "source": "aws.securityhub",
  "account": "<Dán AWS ID Vào Đây>",
  "time": "2026-07-09T13:35:00Z",
  "region": "ap-southeast-1",
  "detail": {
    "findings": [
      {
        "AwsAccountId": "<Dán AWS ID Vào Đây>",
        "Id": "arn:aws:securityhub:ap-southeast-1:<Dán AWS ID Vào Đây>:finding/iam-revoke",
        "Severity": {
          "Product": 8
        },
        "Title": "IAM:AccessKey/Exposed",
        "Description": "IAM Access Key found on GitHub.",
        "Resources": [
          {
            "Type": "AwsIamAccessKey",
            "Id": "arn:aws:iam::629068383761:access-key/<Dán Access Key Vào Đây>",
            "Region": "ap-southeast-1"
          }
        ]
      }
    ]
  }
}
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh8.png)

---

## Bước 3: Theo dõi Step Functions

Workflow mong đợi:

```
Parse Finding
      ↓
Check Severity
      ↓
Revoke IAM
      ↓
Send Notification
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh9.png)

IAM User Account Phụ tạo access key

![Image](/images/5-Workshop/5.9-Test-Validation/anh12.png)

Sau khi triển khai tấn công thì lambda Ivoke IAM thực hiện thu hồi Access Key

![Image](/images/5-Workshop/5.9-Test-Validation/anh13.png)


---

## Bước 4: Kiểm tra CloudWatch Logs

```
/aws/lambda/dev_revoke_iam
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh10.png)

---

## Bước 5: Kiểm tra Email

Kiểm tra email thông báo Access Key đã bị vô hiệu hóa.

![Image](/images/5-Workshop/5.9-Test-Validation/anh11.png)

---

## Kết quả mong đợi

- Lambda Revoke IAM được thực thi.
- Access Key bị Disable/Delete theo thiết kế.
- CloudWatch ghi log.
- SNS gửi Email thành công.

---

# 3. Kiểm thử Critical Unsupported Resource - Skip Automated Action

## Kịch bản

Một số tài nguyên như Amazon S3 hoặc CloudFront chưa được xây dựng workflow phản ứng tự động.

Để tránh gây ảnh hưởng đến ứng dụng đang hoạt động, hệ thống sẽ không thay đổi cấu hình mà chỉ ghi nhận cảnh báo và gửi thông báo cho quản trị viên.

---

## Bước 1: Mở Step Functions

Làm lại các bước như bước 1.

---

## Bước 2: Dán Event JSON

```json
{
  "version": "0",
  "id": "33333333-3333-3333-3333-333333333333",
  "detail-type": "Security Hub Findings - Imported",
  "source": "aws.securityhub",
  "account": "<Dán AWS ID>",
  "time": "2026-07-09T13:35:00Z",
  "region": "ap-southeast-1",
  "detail": {
    "findings": [
      {
        "AwsAccountId": "<Dán AWS ID>",
        "Id": "arn:aws:securityhub:ap-southeast-1:<Dán AWS ID>:finding/s3-unsupported",
        "Severity": {
          "Product": 9
        },
        "Title": "S3:Bucket/PublicAccess",
        "Description": "nothing",
        "Resources": [
          {
            "Type": "AwsS3Bucket",
            "Id": "<Dán Tên S3 Bucket>",
            "Region": "ap-southeast-1"
          }
        ]
      }
    ]
  }
}
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh14.png)

---

## Bước 3: Theo dõi Execution

Workflow:

```
Parse Finding
      ↓
Check Severity
      ↓
Skip Automated Action
      ↓
Send Notification
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh15.png)

---

## Bước 4: Kiểm tra CloudWatch

Kiểm tra Lambda Skip Action.

![Image](/images/5-Workshop/5.9-Test-Validation/anh16.png)

---

## Bước 5: Kiểm tra Email

![Image](/images/5-Workshop/5.9-Test-Validation/anh17.png)

---

## Kết quả mong đợi

- Workflow không thay đổi tài nguyên.
- Chỉ ghi log.
- Gửi Email cảnh báo.
- Execution thành công.

---

# 4. Kiểm thử High Severity (Human in the Loop)

## Kịch bản

Đối với các cảnh báo mức High (Severity từ 4 đến 6.9), hệ thống không tự động cô lập tài nguyên mà chỉ thu thập thông tin, ghi log và chuyển cảnh báo cho kỹ sư SOC để quyết định.

---

## Bước 1: Mở Step Functions

Lặp lại các bước của phần 1.

---

## Bước 2: Dán Event JSON

```json
{
  "version": "0",
  "id": "44444444-4444-4444-4444-444444444444",
  "detail-type": "Security Hub Findings - Imported",
  "source": "aws.securityhub",
  "account": "<Dán AWS Account ID>",
  "time": "2026-07-09T13:35:00Z",
  "region": "ap-southeast-1",
  "detail": {
    "findings": [
      {
        "AwsAccountId": "<Dán AWS Account ID>",
        "Id": "arn:aws:securityhub:ap-southeast-1:<Dán AWS Account ID>:finding/high-severity",
        "Severity": {
          "Product": 5
        },
        "Title": "IAM:User/PasswordPolicy",
        "Description": "Weak password policy detected.",
        "Resources": [
          {
            "Type": "AwsIamUser",
            "Id": "admin",
            "Region": "ap-southeast-1"
          }
        ]
      }
    ]
  }
}
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh18.png)

---

## Bước 3: Theo dõi Execution

Workflow:

```
Parse Finding
      ↓
Check Severity
      ↓
Human Review
      ↓
Send Notification
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh19.png)

---

## Bước 4: Kiểm tra CloudWatch

![Image](/images/5-Workshop/5.9-Test-Validation/anh20.png)

---

## Bước 5: Kiểm tra Email

![Image](/images/5-Workshop/5.9-Test-Validation/anh21.png)

---

## Kết quả mong đợi

- Không thực hiện remediation.
- Ghi log đầy đủ.
- Gửi Email.
- Chờ kỹ sư SOC xử lý.

---

# 5. Kiểm thử Low Severity (Log and Monitor)

## Kịch bản

Các cảnh báo mức Low chủ yếu được sử dụng cho mục đích quan sát hệ thống (Observability).

Workflow sẽ chỉ ghi log để theo dõi xu hướng sự kiện và không thực hiện bất kỳ hành động tự động nào.

---

## Bước 1: Mở Step Functions

Lặp lại các bước ở phần 1.

---

## Bước 2: Dán Event JSON

```json
{
  "version": "0",
  "id": "55555555-5555-5555-5555-555555555555",
  "detail-type": "Security Hub Findings - Imported",
  "source": "aws.securityhub",
  "account": "<Dán AWS Account ID>",
  "time": "2026-07-09T13:35:00Z",
  "region": "ap-southeast-1",
  "detail": {
    "findings": [
      {
        "AwsAccountId": "<Dán AWS Account ID>",
        "Id": "arn:aws:securityhub:ap-southeast-1:629068383761:finding/low-severity-info",
        "Severity": {
          "Product": 2
        },
        "Title": "CloudTrail:Event/Disabled",
        "Description": "CloudTrail logging is disabled.",
        "Resources": [
          {
            "Type": "AwsCloudTrailTrail",
            "Id": "default-trail",
            "Region": "ap-southeast-1"
          }
        ]
      }
    ]
  }
}
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh22.png)

---

## Bước 3: Theo dõi Execution

Workflow:

```
Parse Finding
      ↓
Check Severity
      ↓
Log and Monitor
```

![Image](/images/5-Workshop/5.9-Test-Validation/anh23.png)

---

## Kết quả mong đợi

- Step Function hoàn thành.
- Không thực hiện remediation.
- Chỉ ghi log CloudWatch.
- Không thay đổi tài nguyên AWS.
