---
title: "Translated Blogs"
date: 2026-06-16
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

This section will list and introduce the blogs you have translated. For example:

###  [Blog 1 - From Hourly Caching to Real-Time Pricing: How Samsung Solved Price Synchronization with AWS Lambda Response Streaming](3.1-Blog1/)
This blog introduces a fascinating case study from the AWS Architecture Blog on how Samsung improved the pricing system on Samsung.com to solve the real-time data synchronization challenge. You will learn about the limitations of the legacy architecture using an hourly Cron Job cache (such as permutation explosion of product variants and up to a 60-minute synchronization lag), why Samsung decided to completely eliminate this intermediate aggregation layer to switch to a Serverless model, and how combining Amazon CloudFront with AWS Lambda Response Streaming helps reduce Time To First Byte (TTFB), ensuring accurate prices directly from the Source of Truth while maintaining performance at a massive scale.

### [Blog 2 - Building Multi-Department RAG with Amazon Bedrock Knowledge Bases and Fine-Grained Access Control](3.2-Blog2/)
This blog introduces how to build a production-ready, secure, and multi-tenant Retrieval-Augmented Generation (RAG) system for enterprises using AWS serverless architecture. You will learn how to solve the critical challenge of data isolation and data leakage among different departments (Finance, Engineering, Executive) sharing a single Knowledge Base. 

The article guides you through an event-driven Ingestion Pipeline (utilizing Amazon S3, EventBridge, SQS, and Lambda to enrich metadata) and a secure Query Pipeline. The core highlight of this architecture is the implementation of **Fine-Grained Access Control (FGAC)** by combining **Amazon Cognito**, **Lambda Authorizers**, and **Amazon Verified Permissions (AVP)**. This ensures that the AI assistant only retrieves and answers based on the specific documents the requesting user is strictly authorized to see, making GenAI adoption safe and compliant with enterprise security standards.

###  [Blog 3 - Can You Log In Without OTP SMS with Amazon Cognito?](3.3-Blog3/)
This blog introduces an interesting case study from the AWS Architecture Blog about combining Amazon Cognito with Vonage to reduce OTP fraud and improve mobile login experience. You will learn about the current risks of OTP SMS (SIM Swap Attack, SMS Interception, Social Engineering, SMS Pumping Fraud, user input errors, and undelivered OTPs), why 20% of users drop off during OTP verification, and how to solve this with a multi-layer security approach.

The article guides you through the architecture using Amazon Cognito CUSTOM_AUTH, Vonage Identity Insights, Silent Authentication, and Fraud Defender to create a passwordless, risk-based authentication system that lets users log in in under 5 seconds without manual OTP input, while significantly reducing fraud and improving user experience.

