---
title: "Worklog Tuần 9"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
### Mục tiêu Tuần 9:

* Thực hiện code Website GlobalMart (Frontend: Vite/React, Backend: Java Spring Boot, Database: MySQL RDS).
* Cấu hình CI/CD và Container hóa cho Frontend & Backend với Dockerfile, buildspec.yml, appspec.yml, taskdef.json.
* Thiết kế và cấu hình Terraform modules cho toàn bộ hạ tầng AWS.

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
              Thực hiện code Website GlobalMart
            <ul>
              <li>Frontend: Vite/React, Tailwind CSS</li>
              <li>Backend: Java Spring Boot</li>
              <li>Database: MySQL RDS</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>15/06/2026</td>
      <td>15/06/2026</td>
      <td><a href="https://github.com/KENTksl/globalmart-production-cicd/tree/main">Github</a></td>
    </tr>
    <tr>
      <td>3</td>
      <td>
        <ul>
         <li>
              Thực hiện code Website GlobalMart
            <ul>
              <li>Frontend: Vite/React, Tailwind CSS</li>
              <li>Backend: Java Spring Boot</li>
              <li>Database: MySQL RDS</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>16/06/2026</td>
      <td>16/06/2026</td>
      <td><a href="https://github.com/KENTksl/globalmart-production-cicd/tree/main">Github</a></td>
    </tr>
    <tr>
      <td>4</td>
      <td>
        <ul>
           <li>
              Thực hiện code Website GlobalMart
            <ul>
              <li>Frontend: Vite/React, Tailwind CSS</li>
              <li>Backend: Java Spring Boot</li>
              <li>Database: MySQL RDS</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>17/06/2026</td>
      <td>17/06/2026</td>
      <td><a href="https://github.com/KENTksl/globalmart-production-cicd/tree/main">Github</a></td>
    </tr>
    <tr>
      <td>5</td>
      <td>
        <ul>
          <li>
            Cấu hình CI/CD và Container hóa (Frontend & Backend)
            <ul>
              <li>Viết Dockerfile tối ưu để build image cho Frontend và Backend.</li>
              <li>Cấu hình file buildspec.yml phục vụ cho quá trình tự động hóa với AWS CodeBuild.</li>
              <li>Thiết lập file appspec.yml và taskdef.json hỗ trợ chiến lược triển khai Blue/Green trên Amazon ECS Fargate.</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>18/06/2026</td>
      <td>18/06/2026</td>
      <td><a href="https://github.com/KENTksl/globalmart-production-cicd/tree/main">Github</a></td>
    </tr>
    <tr>
      <td>6</td>
      <td>
        <ul>
          <li>
            Thiết kế và cấu hình Terraform modules
            <ul>
              <li>Xây dựng cấu trúc thư viện Terraform với các modules riêng biệt</li>
              <li>Tạo các modules: vpc, iam, ecr, ecs, rds, s3, codepipeline, monitoring, backup</li>
              <li>Cấu hình file main.tf, variables.tf, outputs.tf cho toàn bộ dự án</li>
              <li>Đưa các file cấu hình (appspec.yml, buildspec.yml, taskdef.json) vào dự án</li>
              <li>Thiết lập file terraform.tfvars.example và .gitignore</li>
            </ul>
          </li>
        </ul>
      </td>
      <td>19/06/2026</td>
      <td>19/06/2026</td>
      <td><a href="https://github.com/KENTksl/globalmart-production-cicd/tree/main">Github</a></td>
    </tr>
  </tbody>
</table>


### KẾT QUẢ ĐẠT ĐƯỢC TUẦN 9: CODE WEBSITE, CI/CD & TERRAFORM

1. **Thực hiện code Website GlobalMart**
   - **Frontend**: Phát triển Frontend với Vite/React, Tailwind CSS.
   - **Backend**: Xây dựng Backend với Java Spring Boot.
   - **Database**: Thiết kế kết nối với MySQL RDS.

2. **Cấu hình CI/CD và Container hóa**
   - **Dockerfile**: Viết file Dockerfile tối ưu để build image cho Frontend và Backend.
   - **buildspec.yml**: Cấu hình file buildspec.yml phục vụ cho AWS CodeBuild.
   - **appspec.yml & taskdef.json**: Thiết lập các file hỗ trợ chiến lược triển khai Blue/Green trên Amazon ECS Fargate.

3. **Thiết kế và cấu hình Terraform**
   - **Cấu trúc thư viện**: Xây dựng thành công cấu trúc Terraform với các modules riêng biệt (vpc, iam, ecr, ecs, rds, s3, codepipeline, monitoring, backup).
   - **File cấu hình**: Tạo và cấu hình các file main.tf, variables.tf, outputs.tf.
   - **Quản lý state**: Thiết lập .gitignore và terraform.tfvars.example để quản lý file state và biến môi trường an toàn.
