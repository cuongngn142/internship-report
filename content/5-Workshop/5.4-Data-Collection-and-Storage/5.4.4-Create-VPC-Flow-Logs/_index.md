---
title: 'Create VPC Flow Logs'
date: 2026-07-09
weight: 16
chapter: false
pre: ' <b> 5.4.4. </b> '
---

## Objective

Record network traffic within the VPC.

## Service explanation

VPC Flow Logs capture network traffic information for troubleshooting and anomaly detection.

## Step 1. Create the flow log

- Open the **VPC Console**.
- Select the `soc-platform-vpc` VPC.
- Choose **Flow logs** → **Create flow log**.

![Flow logs create](/images/5-Workshop/placeholder.svg)

## Step 2. Fill in the fields

In the configuration page:

- **Name**: Enter `soc-platform-vpc-flowlog`.
- **Filter**: Select **Reject** (record only rejected traffic).
- **Maximum aggregation interval**: Select **10 minutes**.
- **Destination**: Select **Send to an Amazon S3 bucket**.
- **S3 bucket ARN**: Enter `arn:aws:s3:::soc-platform-logs-<account-id>/vpc-flow-logs/`.
- **Log record format**: Select **Custom format** and add:

```
${version} ${account-id} ${interface-id} ${srcaddr} ${dstaddr} ${srcport} ${dstport} ${protocol} ${packets} ${bytes} ${start} ${end} ${action} ${log-status}
```

- Click **Create flow log**.

![Flow logs form](/images/5-Workshop/placeholder.svg)

## Validation

- The flow log has been created.
- Network traffic is being recorded.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will create an Athena Workgroup and a Glue Database.
