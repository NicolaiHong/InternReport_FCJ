---
title: "Week 5 Worklog"
date: "2025-10-10"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

- Implement advanced networking techniques with VPC Peering and Transit Gateway to interconnect multiple VPCs.
- Deploy a full-stack application using EC2, RDS, Auto Scaling and integrate with CloudFront.
- Build a cost-optimization solution using serverless patterns with AWS Lambda to automate EC2 management.
- Establish a CI/CD pipeline using AWS Developer Tools for automated deployments.
- Configure hybrid cloud storage with AWS Storage Gateway to connect on-premises environments.
- Manage enterprise file systems with Amazon FSx and strengthen web security with AWS WAF.
- Organize AWS resources effectively using Tags and Resource Groups.
- Improve operational skills using both the AWS Management Console and the AWS CLI.

---

### Tasks carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Start Date | Completion Date | Reference Material                                                                                           |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ------------------------------------------------------------------------------------------------------------ |
| 2   | - **Set up VPC Peering between two VPCs:**<br> + Provision the environment using CloudFormation<br> + Create Security Groups for EC2<br> + Launch EC2 instances in each VPC to verify connectivity<br> + Update Network ACLs<br> + Create & accept the Peering connection<br> + Configure Route Tables for routing<br> + Enable Cross-Peer DNS to resolve hostnames<br><br> - **Deploy a hub-and-spoke network using Transit Gateway:**<br> + Create Key Pair<br> + Provision environment using CloudFormation<br> + Create a Transit Gateway as the central connector<br> + Attach VPCs to the Transit Gateway<br> + Configure Transit Gateway Route Tables<br> + Update VPC Route Tables | 10/06/2025 | 10/06/2025      | VPC Peering: <https://000019.awsstudygroup.com/> <br> Transit Gateway: <https://000020.awsstudygroup.com/>   |
| 3   | - **Deploy WordPress on AWS:**<br> + Prepare VPC/Subnets<br> + Create Security Groups for EC2 and RDS<br> + Launch EC2 host for WordPress<br> + Provision RDS for the database<br> + Install and configure WordPress<br> + Set up Auto Scaling<br> + Perform database backup/restore<br> + Integrate CloudFront to improve performance<br><br> - **Optimize EC2 costs with Lambda:**<br> + Tag EC2 instances for cost management<br> + Create IAM Role for Lambda<br> + Write Lambda to automatically stop/start EC2 instances<br> + Test Lambda behavior                                                                                                                                  | 10/07/2025 | 10/07/2025      | WordPress: <https://000021.awsstudygroup.com/> <br> Lambda Optimization: <https://000022.awsstudygroup.com/> |
| 4   | - **Automate application deployment with a CI/CD pipeline:**<br> + Prepare required resources<br> + Install the CodeDeploy Agent on EC2<br> + Create a CodeCommit repository for source code<br> + Configure CodeBuild to build the application<br> + Set up CodeDeploy for automated deployments<br> + Build CodePipeline to orchestrate the pipeline<br> + Troubleshoot pipeline execution issues<br><br> - **Use Storage Gateway for hybrid cloud storage:**<br> + Create an S3 Bucket<br> + Launch an EC2 host for the Storage Gateway appliance<br> + Activate the Storage Gateway<br> + Create file shares<br> + Mount file shares on on-premises machines                           | 10/08/2025 | 10/08/2025      | CI/CD: <https://000023.awsstudygroup.com/> <br> Storage Gateway: <https://000024.awsstudygroup.com/>         |
| 5   | - **Manage Amazon FSx for Windows File Server:**<br> + Create the environment<br> + Provision SSD and HDD Multi-AZ file systems<br> + Create file shares<br> + Run performance tests<br> + Enable Data Deduplication & Shadow Copies<br> + Manage sessions, open files, and quotas<br> + Enable Continuous Access shares<br> + Scale throughput and storage<br> + Delete the environment when finished<br> + Reference AWS CLI for FSx management<br><br> - **Deploy AWS WAF:**<br> + Create an S3 bucket and deploy a sample web app<br> + Use Managed Rules<br> + Create advanced Custom Rules<br> + Test rules<br> + Enable logging<br> + Clean up resources                            | 10/09/2025 | 10/09/2025      | Amazon FSx: <https://000025.awsstudygroup.com/> <br> AWS WAF: <https://000026.awsstudygroup.com/>            |
| 6   | - **Manage resources with Tags & Resource Groups:**<br> + Understand and apply tags in the Console<br> + Launch EC2 with tags<br> + Add/remove tags on resources<br> + Filter resources by tags<br> + Use tags with the AWS CLI<br> + Tag EC2 via CLI<br> + Tag resources at creation via CLI<br> + List tagged resources via CLI<br> + Create Resource Groups based on tags<br> + Manage resources within Resource Groups                                                                                                                                                                                                                                                                 | 10/10/2025 | 10/10/2025      | Tags & Resource Groups: <https://000027.awsstudygroup.com/>                                                  |

---

### Week 5 Achievements:

- Completed advanced networking on AWS:

  - VPC Peering to connect VPCs directly
  - Transit Gateway as a centralized connectivity hub
  - Configured routing and DNS across multiple VPCs

- Deployed and optimized cloud applications:

  - WordPress integrated with RDS
  - Auto Scaling + CloudFront for improved performance and availability
  - Lambda-based automation for EC2 cost optimization

- Built a complete DevOps workflow:

  - Full CI/CD pipeline using CodeCommit – CodeBuild – CodeDeploy – CodePipeline
  - Automated deployment process
  - Hybrid storage solution via Storage Gateway

- Enterprise file management and web security:

  - FSx Multi-AZ setup, quotas management, and deduplication
  - AWS WAF with advanced rule management

- Applied effective resource governance:

  - Cost optimization & resource management using Tags
  - Centralized resource grouping with Resource Groups
  - Advanced operations via both Console & CLI

- Gained hands-on experience with Infrastructure as Code using CloudFormation to create consistent environments.
