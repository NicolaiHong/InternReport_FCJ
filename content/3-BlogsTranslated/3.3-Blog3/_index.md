---
title: "Blog 3"
date: "2025-10-10"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Enhance the local testing experience for serverless applications with LocalStack

> by Patrick Galvin and Debasis Rath

This article announces and explains new capabilities designed to simplify the local testing experience for serverless applications. Through an integration with **AWS Partner**, **LocalStack**, the **AWS Toolkit for Visual Studio Code** now provides a more streamlined way for developers to build, test, and debug their serverless applications without leaving their development environment.

---

## Challenges with Local Serverless Development

While serverless architectures are generally simple to operate and scale, the development and testing process can introduce friction that slows down the code-test-debug cycle. Developers often encounter several common roadblocks:

- **Slow Iteration from Cloud-Based Validation:** Previously, developers had to deploy AWS Serverless Application Model (AWS SAM) templates to the cloud just to test changes, which created significant delays in the feedback loop.
- **Friction from Tool Context Switching:** The need to constantly move between integrated development environments (IDEs), command-line interfaces (CLIs), and resource emulators like LocalStack leads to fragmented and inefficient workflows.
- **Complex Manual Setup:** Manually configuring port mapping and making code edits for local integration tests can introduce inconsistencies between the local and cloud environments.
- **Limited Service Integration Debugging:** Troubleshooting Lambda functions that interact with other AWS services, such as DynamoDB or Amazon SQS, has traditionally required complex manual configuration, extending the time needed to resolve issues.

---

## Automated Setup Process

The LocalStack VSCode Extension can be installed directly from the AWS Toolkit, which provides an intelligent wizard for a streamlined setup. This wizard automatically detects if LocalStack is configured and guides the user through the process. It also handles authentication through a browser-based flow and securely stores the token. Furthermore, the wizard checks for and creates the necessary AWS CLI profiles for LocalStack, allowing developers to easily switch between their local and cloud environments.

![First](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2025/09/12/ComputeBlog-2372-image-4.gif)

---

## Testing a Serverless Application

The article demonstrates these capabilities with a practical example: an event-driven order processing system that uses API Gateway, Amazon SQS, Lambda, and Amazon Simple Notification Service (Amazon SNS).

![Second](/images/Blog3img1.png)

With the new integration, the entire workflow can be tested locally:

- **Deploy Locally:** The AWS SAM application is deployed to the local LocalStack environment using the LocalStack AWS profile.
  ![Third](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2025/09/13/ComputeBlog-2372-build-deploy-3.gif)
- **Debug Locally:** Developers can set breakpoints in their Lambda function code directly in VS Code and use the integrated debugger to step through the execution as it interacts with other locally emulated services.
  ![Fourth](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2025/09/13/ComputeBlog-2372-debug-2.gif)
- **Validate End-to-End:** The complete workflow, from message ingestion at the API Gateway to the final notification from Amazon SNS, can be tested to confirm all service integrations work correctly before deploying to the cloud.

> For an in-depth technical demonstration of this LocalStack integration, refer to this youtube video.

- {{< youtube e2mokcAzDCY >}}

---

## Best Practices for Local Testing

To make the most of this new workflow, the article recommends a layered and strategic approach to testing. This involves starting with fast, isolated unit tests to validate core logic, and then progressively moving to broader integration and system-level validation.

The recommended testing strategy follows four main steps:

1. Begin with local unit tests to focus on isolated function logic.
2. Proceed to local integration testing using LocalStack to confirm interactions between AWS services.
3. After local validation, test the application in the actual AWS environment to surface issues that cannot be emulated, such as IAM permission mismatches or VPC networking challenges.
4. Finally, conduct performance and load testing in AWS to assess how the application handles real-world traffic.

---

## When to Use Local Versus Cloud Testing

While local testing provides significant speed and cost advantages, it's important to understand its limitations and when to test in the cloud. The following table lists potential use cases for each strategy.

| Testing Scenario                        | Local Testing | Cloud Testing | Reason                                                  |
| --------------------------------------- | ------------- | ------------- | ------------------------------------------------------- |
| Function logic validation               | ✓             |               | Fast feedback for core business logic                   |
| Service integration testing             | ✓             |               | Quick validation of AWS service interactions            |
| Rapid iteration during development      | ✓             |               | Immediate feedback without deployment overhead          |
| Cost-sensitive development environments | ✓             |               | Minimizes cloud resource costs during development       |
| Offline development scenarios           | ✓             |               | No internet connectivity required                       |
| Performance and scalability testing     |               | ✓             | Requires actual AWS infrastructure for accurate results |
| IAM permission validation               |               | ✓             | LocalStack doesn't fully replicate IAM behavior         |
| VPC networking scenarios                |               | ✓             | Network configurations can't be accurately emulated     |
| Production-like load testing            |               | ✓             | Real performance metrics only available in AWS          |
| Final validation before deployment      |               | ✓             | Supports compatibility with actual AWS environment      |

---

## Conclusion

The integration of LocalStack into the AWS Toolkit for VS Code significantly enhances the local development experience for serverless applications. By allowing developers to run and debug complex, multi-service applications directly in their IDE, this new capability helps reduce context switching, catch issues earlier, and lower development costs. This leads to faster test cycles and higher-quality deployments, all while keeping the developer in full control of their local environment.
