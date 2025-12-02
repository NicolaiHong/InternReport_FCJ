---
title: "Week 11 Worklog"
date: "2025-12-05"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

- Participate in AWS community events to gain insights into advanced cloud architectures and industry standards.
- Engineer a serverless backend for text services, focusing on DynamoDB schema design and IAM role security.
- Program efficient database retrieval logic featuring pagination and complex filter expressions.
- Architect an in-memory caching strategy and robust API request validation mechanisms.
- Integrate Generative AI capabilities using Amazon Bedrock Agents for dynamic content generation.
- Implement comprehensive observability and debugging for serverless workloads.
- Construct scalable GraphQL APIs utilizing AWS AppSync and DynamoDB resolvers.

### Tasks carried out this week:

| Day | Task                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Start Date | Completion Date | Reference Material                                                                                                                            |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| 2   | - **Participation in "AWS Cloud Mastery Series #2"**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | 11/17/2025 | 11/17/2025      |                                                                                                                                               |
| 3   | - **Provision Serverless Infrastructure for Text Service:** <br>&emsp; + Deploy DynamoDB table `wordsntexts` with a string partition key for storage <br>&emsp; + Configure IAM execution roles permitting `dynamodb:Scan`, `dynamodb:Query`, and logging <br>&emsp; + Initialize Lambda handler skeleton and establish `boto3` database connections <br><br> - **Develop Data Retrieval Algorithms:** <br>&emsp; + Implement `fetch_words_from_db` utilizing scan operations with `LastEvaluatedKey` pagination <br>&emsp; + Create `fetch_paragraph_from_db` applying attributes filtering for content type and length                                                                                                                                                                        | 11/18/2025 | 11/18/2025      |                                                                                                                                               |
| 4   | - **Implement Caching and Data Processing Logic:** <br>&emsp; + Architect a global in-memory cache with a 300-second TTL to optimize read costs <br>&emsp; + Code `get_random_words` to sample data from either cache or database sources <br>&emsp; + Code `get_paragraph` to handle quantity clamping (1-3) and text splitting logic <br><br> - **Engineer API Validation and Response Formatting:** <br>&emsp; + Develop a `Decimal_encoder` class to serialize DynamoDB numeric types for JSON <br>&emsp; + Implement validation for query parameters `type` and `count` to catch `TypeError`/`ValueError` <br>&emsp; + Standardize JSON responses with correct HTTP headers and status codes                                                                                               | 11/19/2025 | 11/19/2025      |                                                                                                                                               |
| 5   | - **Integrate Amazon Bedrock Agent for GenAI:** <br>&emsp; + Update IAM policies to allow `bedrock:InvokeAgent` on Agent ID `HUEBUXSALX` <br>&emsp; + Instantiate `bedrock-agent-runtime` client and manage `invoke_agent` sessions <br>&emsp; + Program logic to decode streaming byte chunks into a cohesive string response <br><br> - **Execute Prompt Engineering and Model Testing:** <br>&emsp; + Refine trigger prompts to enforce a specific output format (three paragraphs with separators) <br>&emsp; + Evaluate underlying models for formatting consistency <br>&emsp; + Implement parsing logic to segment the AI-generated text                                                                                                                                                 | 11/20/2025 | 11/20/2025      |                                                                                                                                               |
| 6   | - **Monitor and Debug via CloudWatch and X-Ray** <br>&emsp; + Audit Lambda logs in CloudWatch to diagnose execution failures <br>&emsp; + Define custom metrics to track specific application performance indicators <br>&emsp; + Set up CloudWatch Alarms to alert on critical metric deviations <br>&emsp; + Activate AWS X-Ray tracing to map service dependencies and latency <br><br> - **Build GraphQL APIs with AWS AppSync** <br>&emsp; + Provision AppSync instance and link DynamoDB as a datasource <br>&emsp; + Develop resolvers for atomic Write and Read operations <br>&emsp; + Implement Update and Delete resolvers for data lifecycle management <br>&emsp; + Configure Scan/Query resolvers for bulk retrieval <br>&emsp; + Design complex resolvers for nested data fields | 11/21/2025 | 11/21/2025      | CloudWatch and X-Ray Monitoring: <br> <https://000085.awsstudygroup.com/> <br> AppSync GraphQL APIs: <br> <https://000086.awsstudygroup.com/> |

### Week 11 Achievements:

- Participated in the "AWS Cloud Mastery Series #2" to acquire knowledge on advanced AWS services and architectural patterns.

- Engineered the serverless infrastructure for a typing practice application:

  - Provisioned DynamoDB table `wordsntexts` to house ~64,726 items using a string partition key.
  - Secured the backend with granular IAM roles for DynamoDB access and CloudWatch logging.
  - Configured optimized Lambda handlers (128 MB, 15s timeout) with persistent `boto3` connections.

- Programmed advanced data retrieval algorithms:

  - Implemented `fetch_words_from_db` utilizing efficient pagination via `LastEvaluatedKey`.
  - Built `fetch_paragraph_from_db` utilizing filter expressions for length categories (Short: 10-25, Medium: 25-60, Long: 60+).

- Optimized performance and request handling:

  - Deployed an in-memory caching mechanism (300s TTL) to minimize DB reads under a load of ~500 requests/hour.
  - Implemented data sampling functions `get_random_words` and `get_paragraph` with input clamping.
  - Created a custom `Decimal_encoder` for JSON serialization and robust input validation to prevent runtime errors.
  - Standardized API responses with correct HTTP status codes and structure.

- Integrated Generative AI via Amazon Bedrock Agents:

  - Configured IAM access for `bedrock:InvokeAgent` targeting Agent ID `HUEBUXSALX`.
  - Developed a runtime client to handle session-based invocation and stream decoding.
  - Engineered prompts to generate structured content (three separated paragraphs) for daily challenges.
  - Implemented parsing logic to seamlessly process AI-generated outputs.

- Established comprehensive monitoring and debugging:

  - Utilized CloudWatch Logs for error analysis and defined custom metrics for performance tracking.
  - Configured CloudWatch Alarms for critical thresholds and enabled X-Ray for distributed tracing.

- Developed a robust GraphQL API layer using AWS AppSync:
  - Integrated DynamoDB data sources and implemented full CRUD resolvers.
  - Enabled bulk data access via Scan/Query resolvers and handled nested structures with complex object resolvers.
