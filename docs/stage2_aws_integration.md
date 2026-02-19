📘 STAGE 2 – AWS Integration Documentation
1️⃣ Objective

- > The objective of Phase 2 was to establish secure connectivity between the FastAPI backend and AWS services to retrieve real-time infrastructure and billing data. This phase focused on integrating EC2, CloudWatch, and Cost Explorer APIs without database persistence.

2️⃣ AWS Services Integrated
✅ Amazon EC2

Purpose:
Retrieve instance metadata including:
- > Instance ID
- > Instance Type
- > Instance State

API Used:
- > describe_instances()


Outcome:
- > Successfully fetched running and stopped instances from AWS account.

✅ Amazon CloudWatch

Purpose:
- > Retrieve performance metrics (CPU utilization) for EC2 instances.

API Used:
- > get_metric_statistics()


Metric:
- > CPUUtilization

Time Range:
- > Last 24 hours

Outcome:
- > Successfully queried CloudWatch metrics. Returned empty list for stopped instances (expected behavior).

✅ AWS Cost Explorer

Purpose:
- > Retrieve daily billing data for forecasting and cost analysis.

API Used:
- > get_cost_and_usage()


Metrics:
- > UnblendedCost

Granularity:
- > Daily

Important Note:
- > Cost Explorer API requires region:

us-east-1

Outcome:
- > Successfully retrieved daily cost data. Estimated flag observed for recent billing period.

3️⃣ IAM Configuration

IAM User Created:
- > cloud-intelligence-app-user

Permission Policy Attached:

- > ReadOnlyAccess (AWS managed policy)


Security Practice:
- > Programmatic access enabled
- > Credentials stored securely in .env
- > No hardcoded credentials in source code
- > .env excluded via .gitignore

4️⃣ Environment Configuration

Environment variables used:
- > AWS_ACCESS_KEY_ID
- > AWS_SECRET_ACCESS_KEY
- > AWS_REGION


Loaded using:
- > python-dotenv

5️⃣ API Endpoints Created for Testing
GET /test-ec2
Returns:
- > List of EC2 instances

GET /test-cpu/{instance_id}
Returns:
- > CPU utilization datapoints

GET /test-cost
Returns:
- > Daily billing data

6️⃣ Observations & Learning

- > CloudWatch does not return metrics for stopped instances.
- > Cost Explorer API must use us-east-1 region.
- > Billing data may show negative or estimated values due to AWS adjustments.
- > IAM permissions must be carefully selected to avoid access errors.

7️⃣ Phase 2 Outcome
At the end of Phase 2, the backend successfully:
- > Connected to AWS securely.
- > Retrieved infrastructure data.
- > Retrieved performance metrics.
- > Retrieved billing information.
- > Validated IAM configuration.
- > Established foundation for data persistence and predictive modeling.

Phase 2 established the Cloud Integration Layer of the system.