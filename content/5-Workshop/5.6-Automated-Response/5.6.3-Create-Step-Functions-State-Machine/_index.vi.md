---
title: 'Tạo Step Functions State Machine'
date: 2026-07-09
weight: 26
chapter: false
pre: ' <b> 5.6.3. </b> '
---

## Mục tiêu

Tạo workflow phản ứng cho các finding bảo mật.

## Giải thích dịch vụ

Step Functions cho phép phối hợp nhiều bước xử lý trong một workflow có thể theo dõi được.

## Bước 1. Tạo IAM role cho Step Functions

Mở **IAM console**, chọn **Roles** → **Create role**

**Select trusted entity**:

- **Trusted entity type**: Chọn **AWS service**
- **Use case**: Chọn **Step Functions**
- Click **Next**

**Add permissions**: Skip (sẽ thêm inline policy)

**Name, review, and create**:

- **Role name**: Nhập `soc-platform-stepfunctions-role`
- Click **Create role**

Thêm inline policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "lambda:InvokeFunction",
      "Resource": [
        "arn:aws:lambda:<region>:<account-id>:function:soc-platform-isolate-ec2",
        "arn:aws:lambda:<region>:<account-id>:function:soc-platform-revoke-iam",
        "arn:aws:lambda:<region>:<account-id>:function:soc-platform-send-notification"
      ]
    }
  ]
}
```

![Step Functions role](/images/5-Workshop/placeholder.svg)

## Bước 2. Tạo state machine

Mở **AWS Step Functions console**, click **Create state machine**

**Choose authoring method**: Chọn **Write your workflow in code**

**Type**: Chọn **Standard**

**Definition**: Paste definition từ file `automated-response.yaml` (phần
SecurityResponseStateMachine)

**State machine settings**:

- **State machine name**: Nhập `soc-platform-security-response`

- **Permissions**: Chọn **Choose an existing role** → `soc-platform-stepfunctions-role`

Click **Create state machine**

![Create state machine](/images/5-Workshop/placeholder.svg)

## Validation

- State machine đã được tạo.
- Workflow có thể chạy khi nhận event.

![Validation](/images/5-Workshop/placeholder.svg)

## Chuyển sang bước tiếp theo

Tiếp theo, bạn sẽ tạo EventBridge rule.
