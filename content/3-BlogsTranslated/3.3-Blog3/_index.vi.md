---
title: "Blog 3"
date: 2026-06-28
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---
# Amazon Cognito Có Thể Đăng Nhập Không Cần OTP SMS?

Mình vừa đọc một bài khá thú vị trên AWS Architecture Blog về cách kết hợp Amazon Cognito với Vonage để giảm gian lận OTP và cải thiện trải nghiệm đăng nhập trên thiết bị di động.

Điều khiến mình ấn tượng là giải pháp này không chỉ tăng cường bảo mật mà còn giúp người dùng đăng nhập mà gần như không cần nhập mã OTP.

---

## Vấn đề của OTP SMS hiện nay

Rất nhiều hệ thống vẫn sử dụng:
Nhập số điện thoại -> Nhận OTP -> Nhập OTP -> Đăng nhập

Tuy nhiên mô hình này tồn tại nhiều rủi ro:
- SIM Swap Attack
- SMS Interception
- Social Engineering
- SMS Pumping Fraud
- Người dùng nhập sai OTP
- OTP không gửi tới thiết bị

Theo số liệu được AWS trích dẫn:
- Khoảng 20% người dùng bỏ cuộc trong bước xác thực OTP
- Tấn công chiếm đoạt tài khoản (ATO) tăng mạnh trong những năm gần đây

---

## Amazon Cognito + Vonage giải quyết như thế nào?

Giải pháp sử dụng Amazon Cognito CUSTOM_AUTH kết hợp với các API của Vonage.

Kiến trúc gồm:
- Amazon CloudFront
- AWS WAF
- Amazon API Gateway
- Amazon Cognito
- AWS Lambda
- Vonage Identity Insights
- Vonage Verify
- Mobile Network Operator

Thay vì tin tưởng hoàn toàn vào OTP, hệ thống đánh giá rủi ro trước khi quyết định phương thức xác thực.

---

## Ba lớp bảo vệ chính

### 1. Identity Insights

Kiểm tra:
- SIM vừa đổi gần đây hay không
- Số điện thoại có hợp lệ không
- Có dấu hiệu tài khoản giả mạo không

Nếu rủi ro cao: Block hoặc Yêu cầu xác thực bổ sung

### 2. Silent Authentication

Đây là phần thú vị nhất.

Thay vì: Gửi OTP -> Người dùng nhập OTP
hệ thống sẽ xác minh trực tiếp với nhà mạng.

Người dùng không cần:
- Đọc mã OTP
- Sao chép OTP
- Nhập OTP

Toàn bộ quá trình diễn ra trong nền và hoàn thành chỉ trong vài giây.

### 3. Fraud Defender

Chống:
- SMS Pumping
- Artificially Inflated Traffic
- Gian lận OTP quy mô lớn

Giúp giảm chi phí gửi SMS không cần thiết.

---

## Luồng đăng nhập thực tế

Quy trình diễn ra như sau:
1. Người dùng nhập số điện thoại.
2. Cognito kích hoạt CUSTOM_AUTH.
3. Lambda gọi Vonage Identity Insights.
4. Hệ thống đánh giá mức độ rủi ro.
5. Nếu an toàn: Silent Authentication được kích hoạt.
6. Nhà mạng xác minh SIM.
7. Cognito phát hành JWT.
8. Người dùng đăng nhập thành công.

Toàn bộ quá trình có thể hoàn thành trong dưới 5 giây mà không cần nhập OTP.

---

## Góc nhìn kiến trúc AWS

Điều mình học được từ case study này không nằm ở Vonage mà nằm ở cách AWS Cognito được mở rộng.

Thông qua CUSTOM_AUTH và Lambda Trigger, Cognito có thể:
- Passwordless Login
- Risk-Based Authentication
- Adaptive Authentication
- MFA tùy chỉnh
- Tích hợp dịch vụ xác thực bên thứ ba

Điều này biến Cognito từ một dịch vụ đăng nhập thông thường trở thành một nền tảng CIAM khá mạnh.

---

## Kết luận

Case study này cho thấy một xu hướng đang phát triển rất nhanh trong lĩnh vực xác thực:

**Giảm tối đa thao tác của người dùng nhưng vẫn tăng cường bảo mật.**

Thay vì bắt mọi người nhập OTP cho mọi phiên đăng nhập, hệ thống sẽ đánh giá rủi ro theo thời gian thực và chỉ yêu cầu xác thực bổ sung khi thực sự cần thiết.

Đây là một hướng tiếp cận rất đáng tham khảo cho các ứng dụng tài chính, thương mại điện tử và mobile-first platform trên AWS.

Bài viết gốc: https://aws.amazon.com/vi/blogs/architecture/reducing-sms-otp-fraud-with-vonage-network-powered-solutions-and-amazon-cognito/
![Blog3](/images/3-Blog/blog3-1.jpg)
![Blog3](/images/3-Blog/blog3-2.jpg)
