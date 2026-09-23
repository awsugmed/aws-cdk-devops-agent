---
name: daily-health-report
description: Daily operational health check across all production accounts
  for ProductA and ProductB products. Checks CloudWatch alarms, ECS service
  health, Lambda error rates, and DynamoDB throttling. Use this skill
  for the scheduled daily-health-report custom SRE agent.
---

# Daily Health Report

Generate a daily operational health summary across all production accounts.

## Step 1: Check active alarms

Query all CloudWatch alarms in ALARM state across:
- aws-prod-product-a (<PRODUCT_A_PROD_ACCOUNT_ID>)
- aws-prod-product-b (<PRODUCT_B_PROD_ACCOUNT_ID>)

## Step 2: ECS service health

For each production ECS cluster, verify:
- Desired count == Running count
- No services in deployment (stuck deploys)
- CPU/Memory utilization below 80%

## Step 3: Lambda error rates

Check Lambda functions with error rate > 1% in the past 24h.
Flag any functions with invocation count = 0 (potential dead code).

## Step 4: DynamoDB throttling

Check for any ConsumedReadCapacityUnits or ConsumedWriteCapacityUnits
exceeding provisioned capacity in the past 24h.

## Step 5: Recent deployments

List deployments that occurred in the past 24h across both products.
Flag any that have not stabilized.

## Output format

Present findings as:
- **Overall status**: HEALTHY / DEGRADED / CRITICAL
- **Issues found**: grouped by product and module
- **Recommendations**: prioritized list of actions
- **No issues**: explicitly state "No issues found" if healthy
