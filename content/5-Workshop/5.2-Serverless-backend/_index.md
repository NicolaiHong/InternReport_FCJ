---
title: "Part 2: Backend Deployment with API Gateway, Lambda, RDS, and Cognito"
date: "2025-09-15"
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

## Introduction

Welcome to the second part in our workshop building serverless application series! In this hands-on session, you'll build a complete, secure backend infrastructure for your serverless application using AWS managed services.

You will then learn how to connect our serverless backend to frontend that we previously built in Part 1

Modern applications require robust, scalable backend systems that can handle business logic, manage data securely, and authenticate users. In this workshop, you'll create a fully serverless backend architecture using AWS Lambda for compute, Amazon RDS for data persistence, API Gateway for RESTful APIs, Amazon Cognito for user authentication, and AWS Secrets Manager for secure credential management.

![Diagram](/images/5-Workshop/diagram.png)

### What You'll Build

By the end of this part, you'll have deployed a complete backend infrastructure featuring:

- **RESTful APIs**: API Gateway endpoints that handle HTTP requests and route them to appropriate Lambda functions
- **Serverless Computing**: Lambda functions written in Node.js/Python that execute your business logic
- **Managed Database**: Amazon RDS PostgreSQL database for reliable data storage
- **User Authentication**: Amazon Cognito user pools for sign-up, sign-in, and user management
- **API Security**: Cognito authorizers protecting your API endpoints.
  Furthermore, enforce API Gateway to only accept requests originated from CloudFront
- **Secrets Management**: AWS Secrets Manager securely storing database credentials and generate a secure value to embed to CloudFront custom header to restrict access to the API Gateway
- **Network Security**: VPC configuration isolating your database from public internet

### Why This Architecture?

This serverless backend architecture offers several key benefits:

- **No Server Management**: AWS handles provisioning, patching, and scaling
- **Pay-Per-Use**: Only pay for actual compute time and storage used
- **Auto-Scaling**: Automatically handles traffic spikes from 0 to thousands of requests
- **Built-in Security**: Multiple layers including IAM, Cognito, VPC, and secrets management
- **Developer Productivity**: Focus on code, not infrastructure

### Workshop Duration

**Estimated Time**: 3-4 hours

- VPC and networking setup: 20 minutes
- RDS database creation: 30 minutes
- Secrets Manager configuration: 15 minutes
- Lambda function development: 45 minutes
- API Gateway setup: 40 minutes
- Cognito configuration: 45 minutes
- Integration and testing: 45 minutes

## Workshop Structure

This workshop is divided into the following sections:

### **Part 1: VPC and Network Setup**

- Create VPC for database isolation
