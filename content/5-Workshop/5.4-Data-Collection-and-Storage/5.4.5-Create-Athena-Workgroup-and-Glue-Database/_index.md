---
title: 'Step 5: Create an Athena Workgroup and Glue Database'
date: 2026-07-09
weight: 17
chapter: false
pre: ' <b> 5.4.5. </b> '
---

## Objective

Create an Athena Workgroup and a Glue Database for querying logs.

## Service explanation

Athena allows you to query data stored directly in Amazon S3 using SQL, while a Glue Database provides the schema for log tables.

## Step 1. Create the Athena Workgroup

- Open the **Athena Console**.
- Select **Workgroups** → **Create workgroup**.

![Athena workgroup](/images/5-Workshop/placeholder.svg)

## Step 2. Fill in the fields

In the configuration page:

- **Workgroup name**: Enter `soc-platform-workgroup`.
- **Query result location**: Enter `s3://soc-platform-logs-<account-id>/athena-results/`.
- **Encrypt query results**: Select **SSE-KMS** and choose the `soc-platform-key`.
- **Publish query metrics to CloudWatch**: Select **Enable**.
- Click **Create workgroup**.

![Athena form](/images/5-Workshop/placeholder.svg)

## Step 3. Create the Glue Database

- Open the **Glue Console**.
- Select **Databases** → **Add database**.

In the configuration page:

- **Database name**: Enter `soc_platform_logs_db`.
- **Description**: Enter `SOC Platform logs database for Athena queries`.
- Click **Create database**.

![Glue DB](/images/5-Workshop/placeholder.svg)

## Validation

- The Athena Workgroup is ready.
- The Glue Database can be used for querying logs.

![Validation](/images/5-Workshop/placeholder.svg)

## Next step

Next, you will enable the detection and compliance services.
