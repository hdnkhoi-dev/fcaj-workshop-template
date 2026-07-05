---
title: "Blog 2"
date: 2026-06-28
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---
# Building Multi-Department RAG with Amazon Bedrock Knowledge Bases and Fine-Grained Access Control

I just read a really interesting article on the AWS Blog about building an internal enterprise GenAI system, where multiple departments share a single Knowledge Base while still ensuring each person only sees the data they're authorized to access.

This is a very practical problem when deploying an AI Assistant in an enterprise.

## The Problem

Suppose a company has multiple departments:
- Finance
- Engineering
- Executive

Each department stores its own documents:
- Financial reports
- System architecture documents
- Incident Reports
- Business strategies
- M&A Planning

However, when deploying an internal AI Chatbot using RAG (Retrieval-Augmented Generation), a major problem arises:
**How can AI answer with correct information without leaking data between departments?**

For example:
- Engineering employees cannot see financial reports.
- Finance cannot see M&A documents.
- Executive can see more types of documents.

---

## Ingestion Pipeline Architecture

To get documents into the Knowledge Base, AWS proposes a quite interesting serverless pipeline.

Workflow:
1. Documents are uploaded to Amazon S3.
2. S3 generates an event to Amazon EventBridge.
3. EventBridge sends a message to Amazon SQS.
4. AWS Lambda processes metadata.
5. Metadata is attached to the document.
6. EventBridge Schedule triggers Lambda Ingest periodically.
7. Lambda ingests data into Amazon Bedrock Knowledge Bases.
8. Embeddings are stored in Amazon S3 Vectors.

Some AWS services in this architecture:
- Amazon S3
- Amazon EventBridge
- Amazon SQS
- AWS Lambda
- Amazon Bedrock Knowledge Bases
- Amazon S3 Vectors
- Amazon CloudWatch

What I like about this architecture is that the entire ingestion process is designed in an event-driven and serverless manner, helping reduce operational costs.

---

## Query Architecture

After data is indexed into the Knowledge Base, users will interact via a web application.

Processing flow:
1. User accesses the application.
2. Amazon CloudFront delivers content.
3. Amazon Cognito authenticates the user.
4. AWS WAF protects the application from common attacks.
5. Amazon API Gateway receives the request.
6. Lambda Authorizer checks access permissions.
7. Amazon Verified Permissions evaluates access policies.
8. AWS Lambda Middleware handles business logic.
9. Amazon Bedrock Knowledge Bases performs data queries.
10. Results are returned to the user.

---

## Most Notable Point: Fine-Grained Access Control

The best thing I see in this architecture is the combination of:
- Amazon Cognito
- Lambda Authorizer
- Amazon Verified Permissions

to create a detailed permission mechanism.

Instead of just checking:
- Is the user logged in?

the system also checks:
- Which department does the user belong to?
- Are they allowed to view this document?
- Are they allowed to query this data?

This helps deploy RAG much more safely in an enterprise environment.

---

## What I Learned

Through this article, I see that when building a GenAI system for an enterprise, the hardest part isn't LLM or Prompt Engineering.

The real challenge lies in:
- Data management
- Metadata
- Access permission control
- Internal information security

AWS is solving this problem by combining:
- Amazon Bedrock Knowledge Bases
- Amazon S3 Vectors
- Amazon Cognito
- Amazon Verified Permissions

to create a RAG platform that's both scalable and secure.

---

## Conclusion

If you're learning about GenAI on AWS, this is a very worthwhile case study because it doesn't just talk about AI, it also shows how to build a complete production-ready RAG system.

Especially, I see the combination between Amazon Bedrock Knowledge Bases and Amazon Verified Permissions as a very suitable approach for enterprises with many departments and strict data permission requirements.

Original post: https://aws.amazon.com/vi/blogs/architecture/secure-multi-tenant-rag-with-amazon-bedrock-and-verified-permissions/

![Blog2](/images/3-Blog/blog2-1.jpg)
![Blog2](/images/3-Blog/blog2-2.jpg)
![Blog2](/images/3-Blog/blog2-3.jpg)
