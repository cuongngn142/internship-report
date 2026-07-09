---
title: 'Create a Step Functions State Machine'
date: 2026-07-09
weight: 26
chapter: false
pre: ' <b> 5.6.3. </b> '
---

## Objective

Create an automated response workflow for security findings.

## Service explanation

AWS Step Functions coordinates multiple processing steps into a trackable workflow.

## Step 1. Create the IAM role for Step Functions

Open the **IAM Console**, then select **Roles** → **Create role**.

**Select trusted entity**:

- **Trusted entity type**: Select **AWS service**.
- **Use case**: Select **Step Functions**.
- Click **Next**.

**Add permissions**:

- Skip this step (an inline policy will be added later).

**Name, review, and create**:

- **Role name**: Enter `soc-platform-stepfunctions-role`.
- Click **Create role**.

Add the following inline policy:

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

![Step Functions role](/images/5-Workshop/5.6-Automated-response/create-stepf-role.png)

## Step 2. Create the state machine

Open the **AWS Step Functions Console**, then click **Create state machine**.

**Choose authoring method**:

- Select **Write your workflow in code**.

**Type**:

- Select **Standard**.

**Definition**:

- Paste the state machine definition from the `automated-response.yaml` file (the **SecurityResponseStateMachine** section).

**State machine settings**:

- **State machine name**: Enter `soc-platform-security-response`.
- **Permissions**: Select **Choose an existing role** → `soc-platform-stepfunctions-role`.

Click **Create state machine**.

![Create state machine](/images/5-Workshop/5.6-Automated-response/create-state-machine.png)

## Validation

- The state machine has been created.
- The workflow can run when an event is received.

![Validation](/images/5-Workshop/5.6-Automated-response/stepf-sec-response.png)

## Next step

Next, you will create an EventBridge rule.
