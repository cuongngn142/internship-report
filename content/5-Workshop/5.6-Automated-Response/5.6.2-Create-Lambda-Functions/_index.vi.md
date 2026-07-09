---
title: 'Tạo Lambda Functions'
date: 2026-07-09
weight: 25
chapter: false
pre: ' <b> 5.6.2. </b> '
---

## Mục tiêu

Tạo 3 Lambda function để xử lý phản ứng tự động.

## Giải thích dịch vụ

Lambda cho phép chạy code mà không cần quản lý server.

## Bước 1. Tạo IAM role cho Lambda

Mở **IAM console**, chọn **Roles** → **Create role**

**Select trusted entity**:

- **Trusted entity type**: Chọn **AWS service**
- **Use case**: Chọn **Lambda**
- Click **Next**

**Add permissions**:

- Attach policy: `AWSLambdaBasicExecutionRole`
- Click **Next**

**Name, review, and create**:

- **Role name**: Nhập `soc-platform-lambda-execution-role`
- Click **Create role**

Thêm inline policy cho SOC operations:

- Chọn role vừa tạo → **Add permissions** → **Create inline policy**
- JSON:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeInstances",
        "ec2:DescribeSecurityGroups",
        "ec2:ModifyInstanceAttribute",
        "ec2:CreateSnapshot",
        "ec2:CreateTags"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "iam:ListAccessKeys",
        "iam:UpdateAccessKey",
        "iam:DeleteLoginProfile",
        "iam:PutUserPolicy",
        "iam:ListUserPolicies",
        "iam:GetUser"
      ],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::soc-platform-logs-<account-id>/incident-logs/*"
    },
    {
      "Effect": "Allow",
      "Action": "sns:Publish",
      "Resource": [
        "arn:aws:sns:<region>:<account-id>:soc-platform-critical-alerts",
        "arn:aws:sns:<region>:<account-id>:soc-platform-high-alerts"
      ]
    }
  ]
}
```

- Click **Create policy**

![Lambda role](/images/5-Workshop/placeholder.svg)

## Bước 2. Tạo Lambda `soc-platform-isolate-ec2`

Mở **AWS Lambda console**, click **Create function**:

**Basic information**:

- **Function name**: Nhập `soc-platform-isolate-ec2`
- **Runtime**: Chọn **Python 3.11**
- **Execution role**: Chọn **Use an existing role** → `soc-platform-lambda-execution-role`
- Click **Create function**

**Code source**: Paste code từ file `automated-response.yaml` (phần IsolateEC2Function)

**Configuration** → **Environment variables**:

- `ISOLATION_SG_ID`: ID của `soc-platform-isolation-sg`
- `LOG_BUCKET`: `soc-platform-logs-<account-id>`

**Configuration** → **General configuration**:

- **Timeout**: 5 minutes

Click **Deploy**

![Lambda isolate](/images/5-Workshop/placeholder.svg)

## Bước 3. Tạo Lambda `soc-platform-revoke-iam`

Lặp lại các bước tương tự:

- **Function name**: `soc-platform-revoke-iam`
- **Environment variables**: `LOG_BUCKET`
- Code từ phần RevokeIAMFunction

![Lambda revoke IAM](/images/5-Workshop/placeholder.svg)

## Bước 4. Tạo Lambda `soc-platform-send-notification`

Lặp lại các bước tương tự:

- **Function name**: `soc-platform-send-notification`
- **Environment variables**:
  - `CRITICAL_TOPIC_ARN`: ARN của critical alerts topic
  - `HIGH_TOPIC_ARN`: ARN của high alerts topic
- Code từ phần SendNotificationFunction

![Lambda notify](/images/5-Workshop/placeholder.svg)

## Validation

- 3 Lambda function đã được tạo.
- Các function có thể được gọi bởi workflow phản ứng.

![Validation](/images/5-Workshop/placeholder.svg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo Step Functions state machine.
