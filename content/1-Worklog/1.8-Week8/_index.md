---
title: "Week 8 Worklog"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---
### Week 8 Objectives:

* Research & Project Planning: Deeply analyze 5 core workflows of GlobalMart to translate into technical specifications and calculate project costs.
* Visual Architecture Design (Draw.io): Build a production-ready overall architecture diagram, clearly showing the Multi-AZ model, Subnet layering and traffic/data flow paths.
* Build Technical Documentation: Complete detailed documentation describing network architecture, CI/CD mechanisms, High Availability solutions for Data tier and monitoring/backup scenarios.


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
            Calculate project costs on AWS Pricing Calculator
            <ul>
              <li><strong>Amazon ECS Fargate (Frontend):</strong> $8.50/month (2 tasks, 0.25 vCPU, 512 MB, running 24/7).</li>
                <li><strong>Amazon ECS Fargate (Backend):</strong> $20.73/month (2 tasks, 0.5 vCPU, 1 GB, running 24/7).</li>
                <li><strong>Public IPv4 (ECS + ALB + NAT):</strong> $29.20/month (8 public IP addresses × $0.005/hour).</li>
                <li><strong>NAT Gateway (AZ-A):</strong> $43.37/month (730 hours, ~5 GB data processed).</li>
                <li><strong>NAT Gateway (AZ-B):</strong> $43.37/month (730 hours, ~5 GB data processed).</li>
                <li><strong>ALB Internet-facing:</strong> $24.24/month (730 hours, ~1 LCU/hour).</li>
                <li><strong>ALB Internal:</strong> $19.40/month (730 hours, minimum LCU).</li>
                <li><strong>Data Transfer Out:</strong> $0.45/month (~5 GB to Internet).</li>
                <li><strong>Data Transfer Cross-AZ:</strong> $0.10/month (~10 GB from Frontend to Backend in different AZ).</li>
                <li><strong>RDS MySQL Multi-AZ (db.t3.micro):</strong> $34.84/month (Primary + Standby, running 24/7).</li>
                <li><strong>RDS Storage:</strong> $5.52/month (20 GB gp2 × 2 AZ).</li>
                <li><strong>RDS Proxy:</strong> $21.90/month (minimum 2 vCPU, 730 hours).</li>
                <li><strong>Secrets Manager:</strong> $0.41/month (1 secret, API calls).</li>
                <li><strong>RDS Snapshot Export to S3:</strong> $0.24/month (~20 GB exported).</li>
                <li><strong>CodePipeline:</strong> $1.00/month (1 active pipeline).</li>
                <li><strong>CodeBuild:</strong> $1.25/month (~50 builds × 5 minutes, general1.small).</li>
                <li><strong>Amazon ECR (Frontend + Backend):</strong> $0.58/month (4 GB storage, ~100 pulls).</li>
                <li><strong>S3 Artifact Bucket:</strong> $0.04/month (1 GB, 1,000 requests).</li>
                <li><strong>S3 Backup Bucket:</strong> $0.58/month (20 GB, transition to Glacier after 30 days).</li>
                <li><strong>CloudWatch Logs:</strong> $3.95/month (5 GB ingestion, container logs + ALB + VPC Flow).</li>
                <li><strong>CloudWatch Metrics & Alarms:</strong> $6.60/month (20 metrics, 8 alarms).</li>
                <li><strong>CloudWatch Dashboard:</strong> $3.00/month (1 dashboard, 9 widgets).</li>
                <li><strong>AWS Backup:</strong> $1.95/month (daily + weekly backup schedule, ~30 GB vault).</li>
                <li><strong>Amazon SNS:</strong> $0.00/month (under 1,000 email notifications, free tier).</li>
                <li><strong>Amazon EventBridge:</strong> $0.00/month (under 1 million events/month, free tier).</li>
                <li><strong>Total:</strong> $271.22/month</li>
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
             Design visual architecture (Draw.io)
            <ul>
               <li>Standardized design: Successfully designed a comprehensive visual diagram for GlobalMart system on Draw.io, accurately describing the closed infrastructure structure in VPC Multi-AZ model along with connections to services outside VPC.</li>
              <li>Standardized interaction flow: Identified and clarified relationships, traffic paths by numbering 15 logical interaction steps on the diagram (from when Dev pushes code until system alerts and backup activation).</li>
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
            Revise project architecture based on Admin's feedback
            <ul>
              <li>Revise number of flows</li>
              <li>Add internal ALB for FE to send API requests to BE</li>
              <li>Update IGW, ECR new icons</li>
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
            Summarize GlobalMart project overview
              <ul>
                <li><strong>Project introduction:</strong> GlobalMart is a simulated DevOps/Platform Engineering production-grade infrastructure project on AWS, applying Multi-AZ High Availability architecture.</li>
                <li><strong>5 core workflows:</strong></li>
                <li>1. Build & Containerization Flow: Automated CI/CD (GitHub → CodePipeline → CodeBuild → ECR/S3)</li>
                <li>2. Deployment & Application Runtime: VPC Multi-AZ, ALB, ECS Fargate (separate FE/BE)</li>
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
            Plan 1-month project implementation
               <ul>
                <li><strong>Week 1 - Core Network & Security Layers</strong>: Research requirements, establish detailed IAM Roles permissions. Initialize VPC Multi-AZ core network with 4 Subnets, configure 2 independent NAT Gateways to avoid SPOF and assign 2 separate Private Route Tables for each AZ. Build security matrix with 6 Security Groups (including sg-rds-proxy).</li>
                <li><strong>Week 2 - Containerization & CI/CD Automation Prep</strong>: Initialize Frontend and Backend ECR repositories with scan-on-push enabled. Write pipeline configuration and definition files (buildspec.yml, appspec.yml, taskdef.json). Initialize S3 Artifact Bucket with versioning and 30-day lifecycle policy. Configure CodeBuild Project with Privileged mode for Docker packaging.</li>
                <li><strong>Week 3 - Container Runtime & Traffic Routing</strong>: Configure complete 3-stage CodePipeline. Initialize ECS Fargate Cluster with Container Insights and detailed Task Definitions. Set up Public ALB pair (attached to 2 Target Groups for Blue/Green) and Internal ALB running across 2 AZs. Implement advanced CodeDeploy configuration.</li>
                <li><strong>Week 4 - HA Data Layer, Monitoring System & Disaster Recovery Drill</strong>: Create DB Subnet Group, establish RDS MySQL Multi-AZ system (Primary AZ-A + Standby AZ-B) securing credentials via Secrets Manager. Integrate RDS Proxy for connection pooling. Also configure CloudWatch Logs, centralized Dashboard (9 widgets) and 8 automatic Alarms via SNS. Run DR Drill scenario (RDS Failover under 60 seconds) and perform End-to-End system tests before acceptance.</li>
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


### WEEK 8 ACHIEVEMENTS: GLOBALMART - ARCHITECTURE DESIGN & PROJECT PLANNING

1. **Planning and Cost Calculation**
   - **AWS Pricing Calculator:** Performed detailed cost calculation for the entire GlobalMart infrastructure with an estimated total cost of $271.22/month.
   - **Cost analysis:** Allocated costs for each service (ECS, RDS, ALB, NAT Gateway, CloudWatch, etc.) to ensure cost optimization.

2. **Visual Architecture Design**
   - **Draw.io Diagram:** Built a production-ready overall architecture diagram with VPC Multi-AZ model, clear Public/Private Subnet layering.
   - **Interaction Flow:** Defined 15 workflow steps from when Developer pushes code until system alerts and backup activation.
   - **Feedback Improvements:** Revised project diagram based on feedback (added Internal ALB, updated icons, adjusted number of flows).

3. **Overview, Planning and Documentation**
   - **Summarized 5 core workflows:** Clearly synthesized GlobalMart's 5 core workflows (Build, Deployment, Data, Monitoring, Backup).
   - **1-month planning:** Delivered detailed project implementation roadmap in 4 weeks (from core network, CI/CD, container runtime to HA data layer and monitoring).
   - **Technical documentation:** Completed Week 8 worklog with full information on objectives, tasks, and achievements.

   ![Kiến trúc Triển khai GlobalMart](/images/2-Proposal/globalmart.png)
