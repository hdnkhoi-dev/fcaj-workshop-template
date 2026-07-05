---
title: "Blog 2"
date: 2026-06-28
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---
# Xây dựng RAG đa phòng ban với Amazon Bedrock Knowledge Bases và Fine-Grained Access Control

Mình vừa đọc một bài khá hay trên AWS Blog về cách xây dựng hệ thống GenAI nội bộ cho doanh nghiệp, nơi nhiều phòng ban cùng sử dụng một Knowledge Base nhưng vẫn đảm bảo mỗi người chỉ được xem đúng dữ liệu được cấp quyền.

Đây là một bài toán rất thực tế khi triển khai AI Assistant trong doanh nghiệp.

## Bài toán

Giả sử công ty có nhiều phòng ban:
- Finance
- Engineering
- Executive

Mỗi bộ phận đều lưu trữ tài liệu riêng:
- Báo cáo tài chính
- Tài liệu kiến trúc hệ thống
- Incident Report
- Chiến lược kinh doanh
- M&A Planning

Tuy nhiên khi triển khai AI Chatbot nội bộ bằng RAG (Retrieval-Augmented Generation), một vấn đề lớn xuất hiện:
**Làm sao để AI trả lời đúng thông tin nhưng không làm lộ dữ liệu giữa các phòng ban?**

Ví dụ:
- Nhân viên Engineering không được xem báo cáo tài chính.
- Finance không được xem tài liệu M&A.
- Executive có thể xem nhiều loại tài liệu hơn.

---

## Kiến trúc Ingestion Pipeline

Để đưa tài liệu vào Knowledge Base, AWS đề xuất một pipeline serverless khá thú vị.

Luồng hoạt động:
1. Tài liệu được upload lên Amazon S3.
2. S3 phát sinh sự kiện tới Amazon EventBridge.
3. EventBridge gửi message vào Amazon SQS.
4. AWS Lambda xử lý metadata.
5. Metadata được gắn vào tài liệu.
6. EventBridge Schedule kích hoạt Lambda Ingest định kỳ.
7. Lambda đưa dữ liệu vào Amazon Bedrock Knowledge Bases.
8. Embedding được lưu trong Amazon S3 Vectors.

Một số dịch vụ AWS xuất hiện trong kiến trúc:
- Amazon S3
- Amazon EventBridge
- Amazon SQS
- AWS Lambda
- Amazon Bedrock Knowledge Bases
- Amazon S3 Vectors
- Amazon CloudWatch

Điểm mình thích ở kiến trúc này là toàn bộ quá trình ingestion được thiết kế theo hướng event-driven và serverless, giúp giảm chi phí vận hành.

---

## Kiến trúc truy vấn dữ liệu

Sau khi dữ liệu được index vào Knowledge Base, người dùng sẽ tương tác thông qua ứng dụng web.

Luồng xử lý:
1. Người dùng truy cập ứng dụng.
2. Amazon CloudFront phân phối nội dung.
3. Amazon Cognito xác thực người dùng.
4. AWS WAF bảo vệ ứng dụng khỏi các cuộc tấn công phổ biến.
5. Amazon API Gateway tiếp nhận request.
6. Lambda Authorizer kiểm tra quyền truy cập.
7. Amazon Verified Permissions đánh giá chính sách phân quyền.
8. AWS Lambda Middleware xử lý nghiệp vụ.
9. Amazon Bedrock Knowledge Bases thực hiện truy vấn dữ liệu.
10. Kết quả được trả về cho người dùng.

---

## Điểm đáng chú ý nhất: Fine-Grained Access Control

Điều mình thấy hay nhất trong kiến trúc này là việc kết hợp:
- Amazon Cognito
- Lambda Authorizer
- Amazon Verified Permissions

để tạo cơ chế phân quyền chi tiết.

Thay vì chỉ kiểm tra:
- User có đăng nhập hay không?

hệ thống còn kiểm tra:
- User thuộc phòng ban nào?
- Có được xem tài liệu này không?
- Có được truy vấn dữ liệu này không?

Điều này giúp triển khai RAG trong môi trường doanh nghiệp an toàn hơn rất nhiều.

---

## Kiến thức mình học được

Qua bài viết này mình thấy rằng khi xây dựng hệ thống GenAI cho doanh nghiệp, phần khó nhất không phải là LLM hay Prompt Engineering.

Thách thức thực sự nằm ở:
- Quản lý dữ liệu
- Metadata
- Phân quyền truy cập
- Bảo mật thông tin nội bộ

AWS đang giải quyết bài toán này bằng cách kết hợp:
- Amazon Bedrock Knowledge Bases
- Amazon S3 Vectors
- Amazon Cognito
- Amazon Verified Permissions

để tạo ra một nền tảng RAG vừa mở rộng tốt vừa đảm bảo bảo mật.

---

## Kết luận

Nếu đang tìm hiểu về GenAI trên AWS, đây là một case study rất đáng tham khảo vì nó không chỉ nói về AI mà còn cho thấy cách xây dựng một hệ thống RAG hoàn chỉnh theo hướng production-ready.

Đặc biệt, mình thấy phần kết hợp giữa Amazon Bedrock Knowledge Bases và Amazon Verified Permissions là một hướng tiếp cận rất phù hợp cho các doanh nghiệp có nhiều phòng ban và yêu cầu phân quyền dữ liệu chặt chẽ.

Bài viết gốc: https://aws.amazon.com/vi/blogs/architecture/secure-multi-tenant-rag-with-amazon-bedrock-and-verified-permissions/
![Blog2](/images/3-Blog/blog2-1.jpg)
![Blog2](/images/3-Blog/blog2-2.jpg)
![Blog2](/images/3-Blog/blog2-3.jpg)
