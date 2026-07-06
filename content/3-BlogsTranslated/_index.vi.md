---
title: "Các bài blogs đã dịch"
date: 2026-06-16
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Tại đây sẽ là phần liệt kê, giới thiệu các blogs mà các bạn đã dịch. Ví dụ:

###  [Blog 1 - Từ Cache Theo Giờ Đến Real-Time Pricing: Samsung Giải Quyết Bài Toán Đồng Bộ Giá Với AWS Lambda Response Streaming](3.1-Blog1/)
Bài viết này chia sẻ một case study thú vị từ AWS Architecture Blog về cách Samsung cải tiến hệ thống định giá trên Samsung.com để giải quyết bài toán đồng bộ dữ liệu theo thời gian thực. Bạn sẽ hiểu được những hạn chế của kiến trúc cũ sử dụng bộ nhớ cache qua Cron Job (như bùng nổ tổ hợp biến thể sản phẩm và độ trễ đồng bộ lên tới 60 phút), lý do vì sao Samsung quyết định loại bỏ hoàn toàn tầng trung gian này để chuyển sang mô hình Serverless, và cách kết hợp giữa Amazon CloudFront với AWS Lambda Response Streaming giúp giảm Time To First Byte (TTFB), đảm bảo hiển thị giá chính xác từ Source of Truth mà vẫn tối ưu được hiệu năng ở quy mô lớn.

###  [Blog 2 - Xây dựng RAG đa phòng ban với Amazon Bedrock Knowledge Bases và Fine-Grained Access Control](3.2-Blog2/)
Blog này giới thiệu cách xây dựng hệ thống Retrieval-Augmented Generation (RAG) an toàn, multi-tenant và sẵn sàng cho production cho doanh nghiệp bằng kiến trúc serverless của AWS. Bạn sẽ học cách giải quyết thách thức quan trọng về cách ly dữ liệu và rủi ro rơi rớt dữ liệu giữa các phòng ban khác nhau (Finance, Engineering, Executive) khi cùng chia sẻ một Knowledge Base.

Bài viết hướng dẫn bạn qua Ingestion Pipeline theo hướng event-driven (sử dụng Amazon S3, EventBridge, SQS và Lambda để làm giàu metadata) và Query Pipeline an toàn. Điểm nhấn cốt lõi của kiến trúc này là việc triển khai **Fine-Grained Access Control (FGAC)** bằng cách kết hợp **Amazon Cognito**, **Lambda Authorizers** và **Amazon Verified Permissions (AVP)**. Điều này đảm bảo AI assistant chỉ truy xuất và trả lời dựa trên các tài liệu cụ thể mà người dùng yêu cầu được cấp quyền xem một cách nghiêm ngặt, giúp việc áp dụng GenAI trở nên an toàn và tuân thủ các tiêu chuẩn bảo mật doanh nghiệp.

###  [Blog 3 - Amazon Cognito Có Thể Đăng Nhập Không Cần OTP SMS?](3.3-Blog3/)
Blog này chia sẻ một bài viết khá thú vị trên AWS Architecture Blog về cách kết hợp Amazon Cognito với Vonage để giảm gian lận OTP và cải thiện trải nghiệm đăng nhập trên thiết bị di động. Bạn sẽ tìm hiểu về các rủi ro hiện tại của OTP SMS (SIM Swap Attack, SMS Interception, Social Engineering, SMS Pumping Fraud, người dùng nhập sai OTP, OTP không gửi tới thiết bị), lý do vì sao khoảng 20% người dùng bỏ cuộc trong bước xác thực OTP, và cách giải quyết bài toán này bằng cách tiếp cận ba lớp bảo vệ.

Bài viết hướng dẫn bạn qua kiến trúc sử dụng Amazon Cognito CUSTOM_AUTH, Vonage Identity Insights, Silent Authentication và Fraud Defender để tạo hệ thống xác thực không cần mật khẩu, dựa trên rủi ro giúp người dùng đăng nhập trong dưới 5 giây mà không cần nhập OTP thủ công, đồng thời giảm đáng kể gian lận và cải thiện trải nghiệm người dùng.
