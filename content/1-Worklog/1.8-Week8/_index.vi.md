---
title: "Worklog Tuần 8"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---
### Mục tiêu Tuần 8:

* Nghiên cứu & Lên Kế hoạch Dự án: Phân tích sâu 5 luồng công việc cốt lõi của GlobalMart để cụ thể hóa thành các thông số kỹ thuật và tính toán chi phí dự án.
* Thiết kế Kiến trúc Trực quan (Draw.io): Xây dựng sơ đồ kiến trúc tổng thể đạt chuẩn Production, thể hiện rõ mô hình Multi-AZ, phân lớp Subnet và đường đi của traffic/dữ liệu.
* Xây dựng Tài liệu Kỹ thuật: Hoàn thiện tài liệu mô tả chi tiết kiến trúc mạng, cơ chế CI/CD, giải pháp High Availability cho tầng Data và kịch bản giám sát/sao lưu.


### Các công việc cần thực hiện trong tuần này:
<table>
  <thead>
    <tr>
      <th>Ngày</th>
      <th>Công việc</th>
      <th>Ngày bắt đầu</th>
      <th>Ngày hoàn thành</th>
      <th>Tài liệu tham khảo</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>2</td>
      <td>
      <ul>
        <li>
            Tính toán chi phí dự án trên AWS Pricing Calculator 
            <ul>
              <li><strong>Amazon ECS Fargate (Frontend):</strong> $8.50/tháng (2 tasks, 0.25 vCPU, 512 MB, chạy 24/7).</li>
                <li><strong>Amazon ECS Fargate (Backend):</strong> $20.73/tháng (2 tasks, 0.5 vCPU, 1 GB, chạy 24/7).</li>
                <li><strong>Public IPv4 (ECS + ALB + NAT):</strong> $29.20/tháng (8 địa chỉ IP công khai × $0.005/giờ).</li>
                <li><strong>NAT Gateway (AZ-A):</strong> $43.37/tháng (730 giờ, ~5 GB dữ liệu xử lý).</li>
                <li><strong>NAT Gateway (AZ-B):</strong> $43.37/tháng (730 giờ, ~5 GB dữ liệu xử lý).</li>
                <li><strong>ALB Internet-facing:</strong> $24.24/tháng (730 giờ, ~1 LCU/giờ).</li>
                <li><strong>ALB Internal:</strong> $19.40/tháng (730 giờ, LCU tối thiểu).</li>
                <li><strong>Data Transfer Out:</strong> $0.45/tháng (~5 GB truyền ra Internet).</li>
                <li><strong>Data Transfer Cross-AZ:</strong> $0.10/tháng (~10 GB từ Frontend sang Backend khác AZ).</li>
                <li><strong>RDS MySQL Multi-AZ (db.t3.micro):</strong> $34.84/tháng (Primary + Standby, chạy 24/7).</li>
                <li><strong>RDS Storage:</strong> $5.52/tháng (20 GB gp2 × 2 AZ).</li>
                <li><strong>RDS Proxy:</strong> $21.90/tháng (tối thiểu 2 vCPU, 730 giờ).</li>
                <li><strong>Secrets Manager:</strong> $0.41/tháng (1 secret, lời gọi API).</li>
                <li><strong>RDS Snapshot Export to S3:</strong> $0.24/tháng (~20 GB xuất ra).</li>
                <li><strong>CodePipeline:</strong> $1.00/tháng (1 pipeline đang hoạt động).</li>
                <li><strong>CodeBuild:</strong> $1.25/tháng (~50 lần build × 5 phút, general1.small).</li>
                <li><strong>Amazon ECR (Frontend + Backend):</strong> $0.58/tháng (4 GB lưu trữ, ~100 lần pull).</li>
                <li><strong>S3 Artifact Bucket:</strong> $0.04/tháng (1 GB, 1.000 requests).</li>
                <li><strong>S3 Backup Bucket:</strong> $0.58/tháng (20 GB, chuyển sang Glacier sau 30 ngày).</li>
                <li><strong>CloudWatch Logs:</strong> $3.95/tháng (5 GB ingestion, logs container + ALB + VPC Flow).</li>
                <li><strong>CloudWatch Metrics & Alarms:</strong> $6.60/tháng (20 metrics, 8 alarms).</li>
                <li><strong>CloudWatch Dashboard:</strong> $3.00/tháng (1 dashboard, 9 widgets).</li>
                <li><strong>AWS Backup:</strong> $1.95/tháng (lịch backup hàng ngày + hàng tuần, ~30 GB vault).</li>
                <li><strong>Amazon SNS:</strong> $0.00/tháng (dưới 1.000 email thông báo, free tier).</li>
                <li><strong>Amazon EventBridge:</strong> $0.00/tháng (dưới 1 triệu sự kiện/tháng, free tier).</li>
                <li><strong>Tổng cộng:</strong> $271.22/tháng</li>
            </ul>
          </li>
          </ul>
      </td>
      <td>08/06/2026</td>
      <td>08/06/2026</td>
      <td>
      <a href="https://calculator.aws/#/">https://calculator.aws/#/</a>
      </td>
    </tr>
    <tr>
      <td>3</td>
      <td>
        <ul>
          <li>
             Thiết kế kiến trúc trực quan (Draw.io)
            <ul>
               <li>Bản thiết kế chuẩn hóa: Thiết kế thành công sơ đồ trực quan toàn diện cho hệ thống GlobalMart trên Draw.io, mô tả chính xác cấu trúc hạ tầng khép kín trong mô hình VPC Multi-AZ cùng các liên kết dịch vụ ngoài VPC.</li>
              <li>Chuẩn hóa luồng tương tác: Định vị và làm rõ mối quan hệ, đường đi của traffic thông qua việc đánh số logic 15 bước tương tác trên sơ đồ (từ lúc Dev push code cho đến khi hệ thống cảnh báo và sao lưu kích hoạt).</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>09/06/2026</td>
      <td>09/06/2026</td>
      <td>
      <a href="https://drive.google.com/file/d/1ZryzSNVIUSl4DsNUXgzRtNNIgzyz3hzw/view?usp=sharing">https://drive.google.com/file/d/.../view?usp=sharing</a>
      </td>
    </tr>
    <tr>
      <td>4</td>
      <td>
        <ul>
          <li>
            Sửa lại kiến trúc dự án theo các nhận xét của Admin
            <ul>
              <li>Sửa lại số luồng</li>
              <li>Thêm ALB internal để FE gửi API request tới BE</li>
              <li>Thay icon IGW, ECR mới</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>10/06/2026</td>
      <td>10/06/2026</td>
      <td> <a href="https://drive.google.com/file/d/1ZryzSNVIUSl4DsNUXgzRtNNIgzyz3hzw/view?usp=sharing">https://drive.google.com/file/d/.../view?usp=sharing</a></td>
    </tr>
    <tr>
      <td>5</td>
      <td>
        <ul>
          <li>
            Tóm tắt tổng quan dự án GlobalMart
              <ul>
                <li><strong>Giới thiệu dự án:</strong> GlobalMart là dự án giả lập hạ tầng DevOps/Platform Engineering tiêu chuẩn Production trên AWS, áp dụng kiến trúc Multi-AZ High Availability.</li>
                <li><strong>5 luồng công việc cốt lõi:</strong></li>
                <li>1. Build & Containerization Flow: CI/CD tự động (GitHub → CodePipeline → CodeBuild → ECR/S3)</li>
                <li>2. Deployment & Application Runtime: VPC Multi-AZ, ALB, ECS Fargate (FE/BE tách biệt)</li>
                <li>3. Data Management & Persistence: RDS MySQL Multi-AZ + RDS Proxy</li>
                <li>4. Monitoring & Observability: CloudWatch Logs/Metrics/Alarms + SNS</li>
                <li>5. Recovery & Backup: RDS Snapshot + S3 Backup Bucket</li>
              </ul>
          </li>
        </ul>
      </td>
      <td>11/06/2026</td>
      <td>11/06/2026</td>
      <td></td>
    </tr>
    <tr>
      <td>6</td>
      <td>
        <ul>
          <li>
            Lên kế hoạch thực hiện dự án trong 1 tháng
               <ul>
                <li><strong>Tuần 1 - Cốt lõi Mạng & Bảo mật Phân lớp</strong>: Nghiên cứu yêu cầu, thiết lập hệ thống IAM Roles phân quyền chi tiết. Khởi tạo mạng lõi VPC Multi-AZ gồm 4 Subnets, cấu hình 2 NAT Gateways độc lập để tránh điểm lỗi đơn lẻ (SPOF) và gán 2 Route Tables Private riêng cho từng AZ. Xây dựng ma trận bảo mật đầu quy trình với 6 Security Groups (bao gồm sg-rds-proxy).</li>
                <li><strong>Tuần 2 - Đóng gói & Chuẩn bị Tự động hóa CI/CD</strong>: Khởi tạo các kho lưu trữ ECR Frontend và Backend có bật tính năng scan on push. Viết các file cấu hình và định nghĩa pipeline (buildspec.yml, appspec.yml, taskdef.json). Khởi tạo S3 Artifact Bucket có bật tính năng versioning cùng quy trình vòng đời (lifecycle 30 ngày). Cấu hình CodeBuild Project bật Privileged mode để đóng gói Docker.</li>
                <li><strong>Tuần 3 - Khởi tạo Runtime Container & Định tuyến Lưu lượng</strong>: Cấu hình chuỗi CodePipeline hoàn chỉnh 3 giai đoạn. Khởi tạo cụm ECS Cluster Fargate tích hợp Container Insights cùng hệ thống Task Definitions chi tiết. Thiết lập cặp đôi ALB Public (gắn 2 Target Groups phục vụ Blue/Green) và ALB Internal chạy song song trên 2 AZ. Triển khai cấu hình CodeDeploy nâng cao.</li>
                <li><strong>Tuần 4 - Thiết lập Tầng Dữ liệu HA, Hệ thống Giám sát & Diễn tập Thảm họa</strong>: Tạo DB Subnet Group, thiết lập hệ thống RDS MySQL Multi-AZ (Primary AZ-A + Standby AZ-B) bảo mật thông tin bằng Secrets Manager. Tích hợp cấu hình RDS Proxy quản lý connection pooling. Đồng thời, cấu hình CloudWatch Logs, Dashboard tập trung (9 widgets) cùng bộ 8 Alarms cảnh báo tự động thông qua SNS. Tiến hành chạy kịch bản diễn tập DR Drill (RDS Failover dưới 60 giây) và thực hiện End-to-End Test toàn hệ thống trước khi nghiệm thu.</li>
              </ul>
          </li>
        </ul>
      </td>
      <td>12/06/2026</td>
      <td>12/06/2026</td>
      <td></td>
    </tr>
  </tbody>
</table>


### KẾT QUẢ ĐẠT ĐƯỢC TUẦN 8: GLOBALMART - THIẾT KẾ KIẾN TRÚC & KẾ HOẠCH DỰ ÁN

1. **Kế hoạch và Tính toán chi phí**
   - **AWS Pricing Calculator:** Thực hiện tính toán chi phí chi tiết cho toàn bộ hạ tầng dự án GlobalMart với tổng chi phí ước tính $271.22/tháng.
   - **Phân tích chi phí:** Phân bổ chi phí cho từng dịch vụ (ECS, RDS, ALB, NAT Gateway, CloudWatch, v.v.) để đảm bảo tối ưu chi phí.

2. **Thiết kế kiến trúc trực quan**
   - **Sơ đồ Draw.io:** Xây dựng sơ đồ kiến trúc tổng thể đạt chuẩn Production với mô hình VPC Multi-AZ, phân lớp Public/Private Subnet rõ ràng.
   - **Luồng tương tác:** Định nghĩa 15 bước luồng công việc từ lúc Developer push code cho đến khi hệ thống cảnh báo và sao lưu kích hoạt.
   - **Cải tiến theo phản hồi:** Sửa lại sơ đồ dự án theo nhận xét (thêm ALB Internal, cập nhật icon, điều chỉnh số luồng).

3. **Tổng quan, Kế hoạch và Tài liệu hóa dự án**
   - **Tóm tắt 5 luồng công việc:** Tổng hợp rõ ràng 5 luồng cốt lõi của GlobalMart (Build, Deployment, Data, Monitoring, Backup).
   - **Lên kế hoạch 1 tháng:** Đưa ra lộ trình thực hiện dự án chi tiết trong 4 tuần (từ cốt lõi mạng, CI/CD, container runtime đến tầng dữ liệu HA và giám sát).
   - **Tài liệu kỹ thuật:** Hoàn thiện worklog tuần 8 với đầy đủ thông tin về mục tiêu, công việc và kết quả đạt được.

   ![Kiến trúc Triển khai GlobalMart](/images/2-Proposal/globalmart.png)
