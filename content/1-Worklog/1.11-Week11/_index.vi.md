---
title: "Worklog Tuần 11"
date: 2026-06-29
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---
### Mục tiêu Tuần 11:

* Cấu hình CodeDeploy cho ECS (Rolling/Blue-Green), hoàn thiện Pipeline 3 stage.
* Triển khai API Gateway + VPC Link để expose backend nội bộ.
* Tạo ECS Services Frontend + Backend, bật Auto Scaling.
* Cấu hình CloudWatch Metrics/Logs/Dashboard và CloudWatch Alarms + SNS.
* Thực hiện Backup & Restore test, Security review, Cost review và Go-Live.

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
              CodeDeploy cho ECS (Rolling)
            <ul>
              <li>Tạo CodeDeploy Application loại Amazon ECS, Deployment Group với globalmart-codedeploy-role</li>
              <li>Viết appspec.yml cho Frontend và Backend</li>
              <li>Hoàn thiện CodePipeline thêm Stage 3 Deploy, kết nối với CodeDeploy</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>29/06/2026</td>
      <td>29/06/2026</td>
      <td></td>
    </tr>
    <tr>
      <td>3</td>
      <td>
        <ul>
         <li>
              API Gateway + VPC Link
            <ul>
              <li>Tạo VPC Link loại HTTP API, target ALB Internal, SG sg-vpclink, subnet Private Subnet A</li>
              <li>Tạo API Gateway HTTP API, integration với VPC Link, route ANY /api/{proxy+}</li>
              <li>Bật Access Logs cho API Gateway vào CloudWatch</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>30/06/2026</td>
      <td>30/06/2026</td>
      <td></td>
    </tr>
    <tr>
      <td>4</td>
      <td>
        <ul>
           <li>
              Triển khai ECS Services (Frontend + Backend)
            <ul>
              <li>Tạo ECS Service globalmart-frontend-svc: Fargate, desired count 2, private subnet, SG sg-ecs-tasks, attach tg-frontend, deployment controller CODE_DEPLOY</li>
              <li>Tạo ECS Service globalmart-backend-svc tương tự, attach tg-backend</li>
              <li>Bật Service Auto Scaling: target tracking CPU utilization 60-70%, min 2, max 6</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>01/07/2026</td>
      <td>01/07/2026</td>
      <td></td>
    </tr>
    <tr>
      <td>5</td>
      <td>
        <ul>
          <li>
            CloudWatch Metrics & Logs & Dashboard
            <ul>
              <li>Bật Container Insights cho ECS Cluster</li>
              <li>Bật Access Logs cho cả 2 ALB vào S3 bucket riêng</li>
              <li>Tạo CloudWatch Dashboard tổng hợp: ALB metrics, ECS metrics, RDS metrics, NAT Gateway metrics</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>02/07/2026</td>
      <td>02/07/2026</td>
      <td></td>
    </tr>
    <tr>
      <td>6</td>
      <td>
        <ul>
          <li>
            CloudWatch Alarms + SNS & Backup & Restore & Go-Live
            <ul>
              <li>Tạo SNS Topic globalmart-alerts, subscribe email/SMS</li>
              <li>Tạo CloudWatch Alarms: High CPU ECS, High 5xx ALB, RDS Storage thấp, RDS CPU cao, ECS Task unhealthy</li>
              <li>Cấu hình AWS Backup Plan để export RDS snapshot vào S3 backup bucket, lifecycle rule chuyển sang Glacier sau 30 ngày</li>
              <li>Thực hiện Restore Test: restore snapshot thành RDS tạm, kiểm tra dữ liệu đúng</li>
              <li>Security review checklist: không public SG ngoài ALB, RDS không public IP, secrets không hardcode, S3 không public, IAM least privilege, HTTPS bắt buộc</li>
              <li>Cost review: sử dụng Cost Explorer/Budgets, đặt Budget Alert</li>
              <li>Go-Live: chuyển DNS Route 53 trỏ đến ALB Public, theo dõi Dashboard 24-48h đầu</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>03/07/2026</td>
      <td>03/07/2026</td>
      <td></td>
    </tr>
  </tbody>
</table>


### KẾT QUẢ ĐẠT ĐƯỢC TUẦN 11: DEPLOYMENT, MONITORING & GO-LIVE

1. **CodeDeploy & Full Pipeline**
   - **CodeDeploy**: Tạo thành công Application và Deployment Group, viết appspec.yml đúng định dạng.
   - **Full Pipeline**: Pipeline có 3 stage Source → Build → Deploy, chạy xanh không lỗi, update ECS Service không downtime.

2. **API Gateway & VPC Link**
   - **VPC Link**: Tạo thành công VPC Link kết nối đến ALB Internal.
   - **API Gateway**: HTTP API hoạt động, route đến backend, access logs vào CloudWatch.

3. **ECS Services & Auto Scaling**
   - **Services**: 2 ECS Services chạy, Target Groups healthy, truy cập ALB Public thấy frontend, API trả response thật.
   - **Auto Scaling**: Bật target tracking, scale đúng khi CPU vượt ngưỡng.

4. **CloudWatch Monitoring & Alarms**
   - **Metrics & Logs**: Container Insights, ALB Access Logs, CloudWatch Logs cho ECS/API Gateway đều hoạt động.
   - **Dashboard & Alarms**: Dashboard tổng hợp hiện real-time metrics, alarms trigger gửi SNS email/SNS thật.

5. **Backup, Restore & Go-Live**
   - **Backup**: Automated Backup và AWS Backup Plan hoạt động, snapshot export vào S3.
   - **Restore Test**: Restore thành công RDS tạm, kiểm tra dữ liệu đúng.
   - **Go-Live**: DNS trỏ đến ALB Public, hệ thống ổn định, monitoring theo dõi 24-48h đầu.
