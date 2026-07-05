---
title: "Worklog Tuần 10"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---
### Mục tiêu Tuần 10:

* Dựng xong hạ tầng nền (Foundation): VPC, Subnet, IGW, NAT Gateway, Security Groups.
* Chuẩn bị IAM Roles và S3 Buckets (Artifact + Backup) với bảo mật tối thiểu.
* Thiết lập ECR Repositories, ECS Cluster và ALB (Internet-Facing + Internal).
* Triển khai RDS Single-AZ và CI/CD Pipeline hoàn chỉnh (Source → Build).

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
              Networking: VPC, Subnet, IGW, NAT, Security Groups
            <ul>
              <li>Tạo VPC: CIDR 10.0.0.0/16, tên globalmart-vpc</li>
              <li>Tạo 3 Subnets: Public Subnet A (10.0.1.0/24, ap-southeast-1a), Private Subnet A (10.0.2.0/24, ap-southeast-1a), Private Subnet B (10.0.3.0/24, ap-southeast-1b)</li>
              <li>Tạo IGW và attach vào VPC, Route Table public route 0.0.0.0/0 → IGW, associate với Public Subnet A</li>
              <li>Tạo NAT Gateway trong Public Subnet A, gắn Elastic IP, Route Table private route 0.0.0.0/0 → NAT Gateway, associate với Private Subnet A & B</li>
              <li>Tạo Security Groups theo bảng: sg-alb-public, sg-alb-internal, sg-ecs-tasks, sg-rds, sg-vpclink</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>22/06/2026</td>
      <td>22/06/2026</td>
      <td></td>
    </tr>
    <tr>
      <td>3</td>
      <td>
        <ul>
         <li>
              IAM Roles & S3 Buckets
            <ul>
              <li>Tạo S3 Buckets: globalmart-artifact-bucket-<suffix>, globalmart-backup-bucket-<suffix>, bật Versioning + SSE, Block Public Access ON</li>
              <li>Tạo IAM Roles: globalmart-codebuild-role, globalmart-codepipeline-role, globalmart-codedeploy-role, globalmart-ecs-task-execution-role, globalmart-ecs-task-role</li>
              <li>Lưu DB credentials vào AWS Secrets Manager</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>23/06/2026</td>
      <td>23/06/2026</td>
      <td></td>
    </tr>
    <tr>
      <td>4</td>
      <td>
        <ul>
           <li>
              ECR & ECS Cluster
            <ul>
              <li>Tạo 2 ECR Repositories: globalmart-frontend, globalmart-backend, bật Image scanning on push, Lifecycle Policy giữ 10 image</li>
              <li>Tạo ECS Cluster loại Fargate: globalmart-ecs-cluster</li>
              <li>Viết Task Definition JSON cho Frontend và Backend</li>
              <li>Tạo CloudWatch Log Groups: /ecs/globalmart-frontend, /ecs/globalmart-backend</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>24/06/2026</td>
      <td>24/06/2026</td>
      <td></td>
    </tr>
    <tr>
      <td>5</td>
      <td>
        <ul>
          <li>
            Application Load Balancer (Internet-Facing + Internal)
            <ul>
              <li>Tạo ALB Internet-Facing: globalmart-alb-public, scheme internet-facing, SG sg-alb-public, listener 80 redirect → 443, Target Group tg-frontend</li>
              <li>Tạo ALB Internal: globalmart-alb-internal, scheme internal, SG sg-alb-internal, Target Group tg-backend</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>25/06/2026</td>
      <td>25/06/2026</td>
      <td></td>
    </tr>
    <tr>
      <td>6</td>
      <td>
        <ul>
          <li>
            RDS Single-AZ & CI/CD Pipeline
            <ul>
              <li>Tạo DB Subnet Group gồm Private Subnet B, tạo RDS MySQL Single-AZ (db.t3.medium), SG sg-rds, bật Automated Backups 7 ngày</li>
              <li>Kết nối GitHub via CodeStar Connection, viết buildspec.yml cho Frontend và Backend</li>
              <li>Tạo CodeBuild Project (Privileged mode ON) và CodePipeline 2 stage (Source → Build)</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>26/06/2026</td>
      <td>26/06/2026</td>
      <td></td>
    </tr>
  </tbody>
</table>


### KẾT QUẢ ĐẠT ĐƯỢC TUẦN 10: HẠ TẦNG NỀN & CI/CD

1. **Networking & Security Groups**
   - **VPC & Subnets**: Tạo thành công VPC 10.0.0.0/16, 3 Subnets (Public A, Private A, Private B) across 2 AZ.
   - **Routing**: Cấu hình IGW, NAT Gateway, Route Tables đúng như thiết kế, test NAT hoạt động qua EC2 tạm.
   - **Security Groups**: Tạo 5 SG theo bảng, đảm bảo least privilege cho từng resource.

2. **IAM Roles & S3 Buckets**
   - **S3 Buckets**: Tạo artifact và backup buckets với Versioning, SSE, Block Public Access.
   - **IAM Roles**: Tạo 5 roles với trust policy và permissions tối thiểu.
   - **Secrets Manager**: Lưu DB credentials an toàn, không hardcode.

3. **ECR, ECS & ALB**
   - **ECR Repositories**: 2 repos với scan on push và lifecycle policy.
   - **ECS Cluster**: Cluster Fargate thành công, register 2 task definitions ACTIVE.
   - **ALB**: 2 ALB (public + internal) ở trạng thái Active, Target Groups unhealthy (chờ task chạy).

4. **RDS & CI/CD Pipeline**
   - **RDS**: Instance Single-AZ Available, kết nối thành công từ private subnet.
   - **Pipeline**: CodePipeline chạy xanh Source → Build, push image lên ECR mỗi khi push code.
