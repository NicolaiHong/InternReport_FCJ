---
title: "Week 3 Worklog"
date: "2025-09-20"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

- Complete essential AWS hands-on labs, including Site-to-Site VPN and core EC2 operations.
- Work through and finish all four modules of the AWS Cloud Technical Essentials course.
- Improve proficiency with AWS Console and CLI (credentials, key pairs, region/service navigation).
- Collaborate with product and design teams to analyze and document TypeRush UI/UX from Figma.
- Assess storage options and finalize the decision to adopt a scalable NoSQL model for TextService.
- Prototype MongoDB integration (environment setup, data seeding, service refactoring, validation).
- Establish consistent and effective communication routines with the First Cloud Journey team.

### Tasks carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Start Date | Completion Date | Reference Material                                                                                                         |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | -------------------------------------------------------------------------------------------------------------------------- |
| 2   | - **Lab 03:** AWS Site-to-Site VPN: <br>&emsp; + Built a complete Site-to-Site VPN setup, including a new VPC, a customer gateway EC2 instance, a Virtual Private Gateway, and the VPN connection. <br>&emsp; + Configured the tunnel and validated successful end-to-end connectivity. <br><br> - **Lab 04:** Amazon EC2 Fundamentals: <br>&emsp; + Launched and connected to both Windows Server and Amazon Linux EC2 instances. <br>&emsp; + Deployed a sample “AWS User Management” CRUD application on both platforms. <br>&emsp; + Explored core EC2 capabilities such as instance resizing, EBS snapshot management, and building custom AMIs.                                                                                                                                                                                                                                      | 09/22/2025 | 09/22/2025      | VPN Lab (Lab 03): <br> <https://000003.awsstudygroup.com/> <br> EC2 Lab (Lab 04): <br> <https://000004.awsstudygroup.com/> |
| 3   | - Started the AWS Cloud Technical Essentials course and completed the first 2 modules: <br>&emsp; + **Module 1:** Cloud Foundations & IAM <br>&emsp;&emsp; - Defined cloud computing and its value proposition. <br>&emsp;&emsp; - Compared on-premises workloads with cloud workloads. <br>&emsp;&emsp; - Created an AWS account and explored different interaction methods (Console, CLI, SDK). <br>&emsp;&emsp; - Studied the AWS Global Infrastructure (Regions, Availability Zones). <br>&emsp;&emsp; - Learned and applied IAM best practices. <br>&emsp; + **Module 2:** Compute & Networking <br>&emsp;&emsp; - Reviewed EC2 architecture components. <br>&emsp;&emsp; - Differentiated containers vs virtual machines. <br>&emsp;&emsp; - Explored serverless technologies and their use cases. <br>&emsp;&emsp; - Studied core VPC networking concepts and created a custom VPC. | 09/23/2025 | 09/23/2025      | AWS Cloud Technical Essentials: <br> <https://www.coursera.org/learn/aws-cloud-technical-essentials>                       |
| 4   | - Collaborated with design to document the TypeRush UI/UX: <br>&emsp; + Participated in a cross-functional review session to evaluate the latest Figma flows. <br>&emsp; + Analyzed major screens (login, game, score summary, settings) to understand layout, hierarchy, and interaction patterns. <br>&emsp; + Listed technical feasibility questions and UI considerations for further alignment. <br>&emsp; + Began translating the designs into early component requirements and user stories. <br><br> - Discussed TextService storage approach with the team lead: <br>&emsp; + Compared relational and non-relational storage models for word/sentence data. <br>&emsp; + Presented pros and cons for each approach based on usage patterns. <br>&emsp; + Finalized the decision to adopt a NoSQL solution due to dynamic schema needs and scalability.                            | 09/24/2025 | 09/24/2025      |                                                                                                                            |
| 5   | - Integrated and tested MongoDB for the TextService prototype: <br>&emsp; + Set up a MongoDB environment using Docker. <br>&emsp; + Updated the data seeding script to insert word/sentence documents into MongoDB collections. <br>&emsp; + Refactored TextService logic to read/write data through MongoDB queries. <br>&emsp; + Performed full integration testing to ensure connectivity and correct data operations.                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | 09/25/2025 | 09/25/2025      |                                                                                                                            |
| 6   | - Completed the remaining AWS Cloud Technical Essentials modules: <br>&emsp; + **Module 3:** Storage & Databases <br>&emsp;&emsp; - Compared file, block, and object storage types. <br>&emsp;&emsp; - Studied Amazon S3 concepts and created an S3 bucket. <br>&emsp;&emsp; - Reviewed EBS usage with EC2. <br>&emsp;&emsp; - Explored AWS database services and created a DynamoDB table. <br>&emsp; + **Module 4:** Monitoring & High Availability <br>&emsp;&emsp; - Understood CloudWatch monitoring and alarm basics. <br>&emsp;&emsp; - Learned cost/performance optimization techniques. <br>&emsp;&emsp; - Studied Elastic Load Balancing for traffic routing. <br>&emsp;&emsp; - Compared vertical vs horizontal scaling and built a high-availability setup.                                                                                                                    | 09/26/2025 | 09/26/2025      | AWS Cloud Technical Essentials: <br> <https://www.coursera.org/learn/aws-cloud-technical-essentials>                       |

### Week 3 Achievements:

- **AWS Hands-on Labs Completed:**

  - Built a full Site-to-Site VPN setup (VPC, customer gateway EC2, virtual private gateway, tunnel configuration).
  - Completed EC2 fundamentals including Windows/Linux instances, CRUD app deployment, snapshot handling, and custom AMIs.

- **Completed all 4 modules of AWS Cloud Technical Essentials**  
  (Cloud Foundations/IAM, Compute & Networking, Storage & Databases, Monitoring & High Availability).

- **Improved AWS Console & CLI Practice:**

  - Account setup and IAM credential management.
  - Navigated services and regions efficiently.
  - Worked with key pairs and resource inspection commands.

- **TypeRush UI/UX Documentation:**

  - Reviewed Figma flows and major interface screens.
  - Captured component behaviors and feasibility questions.
  - Drafted early user stories and component specifications.

- **TextService Storage Strategy:**

  - Evaluated SQL vs NoSQL approaches.
  - Chose NoSQL for improved flexibility and scalability.

- **MongoDB Prototype Implementation:**
  - Set up MongoDB via Docker.
  - Updated seeding scripts.
  - Refactored service logic to use MongoDB.
  - Verified smooth end-to-end read/write operations.
