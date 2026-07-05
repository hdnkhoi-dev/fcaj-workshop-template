---
title: "Blog 1"
date: 2026-06-16
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
# From Hourly Caching to Real-Time Pricing: How Samsung Solved Price Synchronization with AWS Lambda Response Streaming

In e-commerce, product pricing is one of the most critical pieces of data. If the price displayed on the product page differs from the price at checkout, the customer experience can be severely impacted.

Recently, I read a very interesting post from the AWS Architecture Blog about how Samsung improved the pricing system on Samsung.com using AWS Lambda Response Streaming and Amazon CloudFront.

This is an excellent case study on choosing the right architecture instead of just focusing on optimizing performance.

---

## The Problem

Samsung.com is Samsung's direct sales channel, offering a wide range of product lines such as phones, TVs, home appliances, and accessories.

During major events like Black Friday, a product listing page may need to display the prices of more than 30 different SKUs at the same time.

Each product has multiple variants:
- Color
- Memory version
- Promotional programs
- Region-specific offers

This makes querying prices in real-time a major challenge.

---

## Legacy Architecture and Issues Arising

In the legacy architecture, Samsung used a Data Aggregation layer between the Pricing Engine and CloudFront.

A Cron Job would run every hour to:
1. Fetch all product data from the Pricing Engine.
2. Pre-calculate all possible price combinations.
3. Save the results into the cache to serve users.

This model helped speed up data read times but created two major problems.

### 1. Permutation Explosion
As the number of products and variants increased, the number of price combinations grew exponentially.

For example: 30 products × multiple versions × multiple promotional programs could generate thousands or tens of thousands of records that needed to be pre-calculated.

As a result, the system consumed a lot of storage and processing resources for data that might never be accessed by users.

### 2. Synchronization Lag
This is the more serious issue.

Because the Cron Job only ran once an hour, the data in the cache could lag behind real-world data by up to 60 minutes.

If a Flash Sale program started at 10:05, customers could still see the old price until the next Cron Job ran at 11:00.

Consequences:
- Inaccurate price display
- Customers surprised at checkout
- Loss of trust in the system
- Impact on revenue

---

## New Solution with AWS Lambda Response Streaming

Instead of continuing to optimize the cache, Samsung decided to completely eliminate the Data Aggregation layer.

The new architecture is built on the principle: **Always fetch data from the primary source (Source of Truth) at the time the user makes the request.**

Operational workflow:
1. The user sends a request to get the product price.
2. Amazon CloudFront checks the cache at the Edge Location.
3. If a cache miss occurs, the request is forwarded to AWS Lambda.
4. Lambda performs a fan-out and sends multiple requests in parallel to the Pricing Engine.
5. The results are streamed back to the user as soon as the data is returned.
6. CloudFront continues to cache the results for a short period to optimize performance.

---

## Why AWS Lambda Response Streaming fits?

Normally, Lambda will wait to finish processing all data before returning a response. This increases the wait time when aggregating data from multiple different sources.

With Lambda Response Streaming:
- Data is sent back as soon as there are results
- Reduces Time To First Byte (TTFB)
- Users receive responses sooner
- No need to build a complex intermediate cache layer

This is the key differentiator that helped Samsung ensure both performance and the accuracy of pricing data.

---

## AWS Services Featured in the Architecture

- Amazon CloudFront
- AWS Lambda
- Lambda Response Streaming
- Lambda Function URL
- Provisioned Concurrency

Although the number of services is not large, the way these services are combined helped solve a real-world problem at a massive scale.

---

## Lessons I Learned from This Case Study

The most interesting thing does not lie in Lambda Response Streaming itself, but in the architectural mindset.

Caching is often seen as the solution to performance problems. However, in problems where data accuracy is more important than retrieval speed, caching can sometimes become the root cause of business logic errors.

Samsung's case study shows that:
- Adding a cache is not always the right direction.
- The Source of Truth needs to be prioritized in systems related to selling prices.
- Serverless can effectively solve real-time data aggregation problems.
- A simpler architecture can sometimes bring better results than a system with multiple intermediate layers.

Original post: https://aws.amazon.com/vi/blogs/architecture/how-samsung-achieved-real-time-pricing-with-aws-lambda-response-streaming/

![Kiến trúc cũ của Samsung gây ra vấn đề trễ đồng bộ](/images/3-Blog/1.jpg)
![Kiến trúc mới sử dụng AWS Lambda Response Streaming của Samsung](/images/3-Blog/2.jpg)
