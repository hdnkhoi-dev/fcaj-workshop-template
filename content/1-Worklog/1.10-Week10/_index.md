---
title: "Week 10 Worklog"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---
### Week 10 Objectives:

* Build foundation infrastructure: VPC, Subnets, IGW, NAT Gateway, Security Groups.
* Prepare IAM Roles and S3 Buckets (Artifact + Backup) with minimum security.
* Set up ECR Repositories, ECS Cluster and ALB (Internet-Facing + Internal).
* Deploy RDS Single-AZ and complete CI/CD Pipeline (Source → Build).

### Tasks to be carried out this week:
<table>
  <thead>
    <tr>
      <th>Day</th>
      <th>Task</th>
      <th>Start Date</th>
      <th>Completion Date</th>
      <th>Reference Material</th>
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
              <li>Create VPC: CIDR 10.0.0.0/16, name globalmart-vpc</li>
              <li>Create 3 Subnets: Public Subnet A (10.0.1.0/24, ap-southeast-1a), Private Subnet A (10.0.2.0/24, ap-southeast-1a), Private Subnet B (10.0.3.0/24, ap-southeast-1b)</li>
              <li>Create IGW and attach to VPC, Public Route Table route 0.0.0.0/0 → IGW, associate with Public Subnet A</li>
              <li>Create NAT Gateway in Public Subnet A, attach Elastic IP, Private Route Table route 0.0.0.0/0 → NAT Gateway, associate with Private Subnet A & B</li>
              <li>Create Security Groups as per table: sg-alb-public, sg-alb-internal, sg-ecs-tasks, sg-rds, sg-vpclink</li>
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
              <li>Create S3 Buckets: globalmart-artifact-bucket-<suffix>, globalmart-backup-bucket-<suffix>, enable Versioning + SSE, Block Public Access ON</li>
              <li>Create IAM Roles: globalmart-codebuild-role, globalmart-codepipeline-role, globalmart-codedeploy-role, globalmart-ecs-task-execution-role, globalmart-ecs-task-role</li>
              <li>Store DB credentials in AWS Secrets Manager</li>
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
              <li>Create 2 ECR Repositories: globalmart-frontend, globalmart-backend, enable Image scanning on push, Lifecycle Policy keep 10 images</li>
              <li>Create Fargate ECS Cluster: globalmart-ecs-cluster</li>
              <li>Write Task Definition JSON for Frontend and Backend</li>
              <li>Create CloudWatch Log Groups: /ecs/globalmart-frontend, /ecs/globalmart-backend</li>
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
              <li>Create Internet-Facing ALB: globalmart-alb-public, scheme internet-facing, SG sg-alb-public, listener 80 redirect → 443, Target Group tg-frontend</li>
              <li>Create Internal ALB: globalmart-alb-internal, scheme internal, SG sg-alb-internal, Target Group tg-backend</li>
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
              <li>Create DB Subnet Group including Private Subnet B, create RDS MySQL Single-AZ (db.t3.medium), SG sg-rds, enable Automated Backups 7 days</li>
              <li>Connect GitHub via CodeStar Connection, write buildspec.yml for Frontend and Backend</li>
              <li>Create CodeBuild Project (Privileged mode ON) and CodePipeline 2 stages (Source → Build)</li>
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


### WEEK 10 ACHIEVEMENTS: FOUNDATION INFRASTRUCTURE & CI/CD

1. **Networking & Security Groups**
   - **VPC & Subnets**: Successfully created VPC 10.0.0.0/16, 3 Subnets (Public A, Private A, Private B) across 2 AZ.
   - **Routing**: Configured IGW, NAT Gateway, Route Tables as designed, tested NAT working via temporary EC2.
   - **Security Groups**: Created 5 SGs as per table, ensuring least privilege for each resource.

2. **IAM Roles & S3 Buckets**
   - **S3 Buckets**: Created artifact and backup buckets with Versioning, SSE, Block Public Access.
   - **IAM Roles**: Created 5 roles with correct trust policy and minimum permissions.
   - **Secrets Manager**: Stored DB credentials securely, no hardcoding.

3. **ECR, ECS & ALB**
   - **ECR Repositories**: 2 repos with scan on push and lifecycle policy.
   - **ECS Cluster**: Fargate cluster successfully created, registered 2 ACTIVE task definitions.
   - **ALB**: 2 ALBs (public + internal) in Active state, Target Groups unhealthy (waiting for tasks).

4. **RDS & CI/CD Pipeline**
   - **RDS**: Single-AZ instance Available, successfully connected from private subnet.
   - **Pipeline**: CodePipeline runs green Source → Build, pushes image to ECR on every code push.
