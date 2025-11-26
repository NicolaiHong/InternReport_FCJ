---
title: "Week 6 Worklog"
date: "2025-11-26"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

- Learn to manage EC2 access control using IAM services with resource tags and permission boundaries.
- Set up and configure monitoring tools including Grafana and AWS CloudWatch.
- Implement AWS Systems Manager for patch management and remote command execution.
- Optimize EC2 instances through right-sizing practices and AWS Compute Optimizer.
- Apply encryption to S3 data using AWS KMS and configure audit logging.
- Analyze AWS costs and usage patterns with Cost Explorer.
- Build a data pipeline and lake using S3, Kinesis, Glue, Athena, and QuickSight.
- Automate infrastructure provisioning with AWS CloudFormation templates.

### Tasks carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Start Date | Completion Date | Reference Material                                                                                                                   |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| 2   | - **Manage access to EC2 services with resource tags through IAM services:** <br>&emsp; + Create an IAM user for preparation <br>&emsp; + Create a custom IAM Policy to define specific permissions <br>&emsp; + Set up an IAM Role to be assumed by users or services <br>&emsp; + Verify the policy by switching roles and testing access <br> <br> - **Getting started with Grafana basic:** <br>&emsp; + Create a VPC and subnet to establish a network environment <br>&emsp; + Configure a Security Group to control inbound and outbound traffic <br>&emsp; + Launch an EC2 instance to host the monitoring application <br>&emsp; + Create an IAM User and Role for secure access to AWS resources <br>&emsp; + Assign the IAM Role to the EC2 instance <br>&emsp; + Install Grafana on the EC2 instance <br>&emsp; + Set up monitoring dashboards within Grafana                    | 10/13/2025 | 10/13/2025      | IAM services: <br> <https://000028.awsstudygroup.com/> <br> Grafana basic: <br> <https://000029.awsstudygroup.com/>                  |
| 3   | - **Limit user permissions with IAM Permission Boundary:** <br>&emsp; + Perform preparatory steps for the exercise <br>&emsp; + Create a restriction policy to define the maximum allowable permissions <br>&emsp; + Create a new IAM user with limited permissions <br>&emsp; + Test the IAM user's limits to verify the permission boundaries <br> <br> - **Manage patches and run commands on multiple servers with AWS System Manager:** <br>&emsp; + Create a VPC and Subnet for the network environment <br>&emsp; + Launch a public Windows EC2 instance <br>&emsp; + Create an IAM Role with necessary permissions <br>&emsp; + Assign the IAM Role to the EC2 instance <br>&emsp; + Configure and use Patch Manager to handle server patching <br>&emsp; + Use Run Command to execute commands on the servers                                                                       | 10/14/2025 | 10/14/2025      | IAM permission boundary: <br> <https://000030.awsstudygroup.com/> <br> AWS Systems Manager: <br> <https://000031.awsstudygroup.com/> |
| 4   | - **Implement right-sizing practices for Amazon EC2:** <br>&emsp; + Get acquainted with Amazon CloudWatch for monitoring <br>&emsp; + Create and attach an IAM Role for the CloudWatch Agent <br>&emsp; + Install the CloudWatch Agent on an EC2 instance <br>&emsp; + Use AWS Compute Optimizer to analyze and optimize EC2 configurations <br> <br> - **Encrypt data at rest in S3 using AWS KMS:** <br>&emsp; + Create necessary IAM policies, roles, groups, and users <br>&emsp; + Set up a Key Management Service (KMS) key <br>&emsp; + Create an S3 bucket and upload data <br>&emsp; + Configure AWS CloudTrail for logging and Amazon Athena for querying data <br>&emsp; + Test and share encrypted data stored in S3                                                                                                                                                             | 10/15/2025 | 10/15/2025      | EC2 right-sizing: <br> <https://000032.awsstudygroup.com/> <br> S3 encryption with KMS: <br> <https://000033.awsstudygroup.com/>     |
| 5   | - **Visualize and analyze costs with AWS Cost Explorer:** <br>&emsp; + View cost and usage data by service and by account <br>&emsp; + Analyze the scope and effectiveness of Savings Plans and Reserved Instances <br>&emsp; + Evaluate cost elasticity <br>&emsp; + Create custom reports for EC2 instances <br>&emsp; + Use Cost Explorer for in-depth cost analysis <br>&emsp; + Review data transfer costs for common architectures <br> <br> - **Build a data lake on AWS:** <br>&emsp; + Create an IAM Role and Policy for necessary permissions <br>&emsp; + Set up an S3 bucket for data storage <br>&emsp; + Create a Kinesis Data Firehose delivery stream for data collection <br>&emsp; + Use a Glue Crawler to create a data catalog <br>&emsp; + Perform data transformation <br>&emsp; + Analyze data using Amazon Athena <br>&emsp; + Visualize data with Amazon QuickSight | 10/16/2025 | 10/17/2025      | AWS Cost Explorer: <br> <https://000034.awsstudygroup.com/> <br> Data lake on AWS: <br> <https://000035.awsstudygroup.com/>          |
| 6   | - **Study AWS CloudWatch for monitoring and observability:** <br>&emsp; + Explore CloudWatch Metrics, including viewing, searching, and using expressions <br>&emsp; + Work with CloudWatch Logs, Logs Insights, and Metric Filters <br>&emsp; + Configure CloudWatch Alarms to trigger notifications <br>&emsp; + Create CloudWatch Dashboards for visualizing data <br> <br> - **Automate infrastructure with AWS CloudFormation:** <br>&emsp; + Create IAM Users and Roles for preparation <br>&emsp; + Develop a basic CloudFormation template to provision resources <br>&emsp; + Explore advanced features like Custom Resources with Lambda <br>&emsp; + Use Mappings, Stacksets, and Drift Detection for complex deployments                                                                                                                                                         | 10/17/2025 | 10/17/2025      | AWS CloudWatch: <br> <https://000036.awsstudygroup.com/> <br> AWS CloudFormation: <br> <https://000037.awsstudygroup.com/>           |

### Week 6 Achievements:

- Successfully managed EC2 access control through IAM services:
  - Configured resource-based access policies using tags
  - Implemented permission boundaries to limit user capabilities
- Set up monitoring and observability infrastructure:
  - Deployed Grafana on EC2 for custom dashboards
  - Configured CloudWatch Metrics, Logs, and Alarms for resource monitoring
- Implemented AWS Systems Manager capabilities:
  - Used Patch Manager for automated server updates
  - Executed remote commands across multiple instances with Run Command
- Applied EC2 optimization and cost management practices:
  - Installed and configured CloudWatch Agent for detailed metrics
  - Analyzed instance configurations using AWS Compute Optimizer
  - Reviewed cost patterns and trends with Cost Explorer
- Secured data storage with encryption:
  - Created and managed KMS keys for S3 encryption
  - Set up CloudTrail and Athena for audit logging and analysis
- Built a complete data lake pipeline:
  - Configured Kinesis Data Firehose for streaming data ingestion
  - Created data catalogs with Glue Crawler
  - Performed data analysis with Athena and visualization with QuickSight
- Automated infrastructure deployment with CloudFormation:
  - Developed templates for resource provisioning
  - Explored advanced features including Lambda-backed custom resources and StackSets
