---
title: "Week 11 Worklog"
date: 2026-06-29
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---
### Week 11 Objectives:

* Configure CodeDeploy for ECS (Rolling/Blue-Green), complete 3-stage Pipeline.
* Deploy API Gateway + VPC Link to expose internal backend.
* Create ECS Services Frontend + Backend, enable Auto Scaling.
* Configure CloudWatch Metrics/Logs/Dashboard and CloudWatch Alarms + SNS.
* Perform Backup & Restore test, Security review, Cost review and Go-Live.

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
            CodeDeploy for ECS (Rolling/Blue-Green)
            <ul>
              <li>Create CodeDeploy Application type Amazon ECS, Deployment Group with globalmart-codedeploy-role</li>
              <li>Write appspec.yml for Frontend and Backend</li>
              <li>Complete CodePipeline adding Stage 3 Deploy, connect to CodeDeploy</li>
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
              <li>Create HTTP API type VPC Link, target Internal ALB, SG sg-vpclink, subnet Private Subnet A</li>
              <li>Create API Gateway HTTP API, integration with VPC Link, route ANY /api/{proxy+}</li>
              <li>Enable Access Logs for API Gateway to CloudWatch</li>
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
            Deploy ECS Services (Frontend + Backend)
            <ul>
              <li>Create ECS Service globalmart-frontend-svc: Fargate, desired count 2, private subnet, SG sg-ecs-tasks, attach tg-frontend, deployment controller CODE_DEPLOY</li>
              <li>Create ECS Service globalmart-backend-svc similarly, attach tg-backend</li>
              <li>Enable Service Auto Scaling: target tracking CPU utilization 60-70%, min 2, max 6</li>
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
              <li>Enable Container Insights for ECS Cluster</li>
              <li>Enable Access Logs for both ALBs to separate S3 bucket</li>
              <li>Create CloudWatch Dashboard aggregating: ALB metrics, ECS metrics, RDS metrics, NAT Gateway metrics</li>
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
              <li>Create SNS Topic globalmart-alerts, subscribe email/SMS</li>
              <li>Create CloudWatch Alarms: High CPU ECS, High 5xx ALB, Low RDS Storage, High RDS CPU, Unhealthy ECS Task</li>
              <li>Configure AWS Backup Plan to export RDS snapshot to S3 backup bucket, lifecycle rule transition to Glacier after 30 days</li>
              <li>Perform Restore Test: restore snapshot to temporary RDS, verify data correctness</li>
              <li>Security review checklist: no public SG except ALB, RDS no public IP, no hardcoded secrets, S3 not public, IAM least privilege, HTTPS enforced</li>
              <li>Cost review: use Cost Explorer/Budgets, set Budget Alert</li>
              <li>Go-Live: update Route 53 DNS to point to Public ALB, monitor Dashboard for first 24-48h</li>
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


### WEEK 11 ACHIEVEMENTS: DEPLOYMENT, MONITORING & GO-LIVE

1. **CodeDeploy & Full Pipeline**
   - **CodeDeploy**: Successfully created Application and Deployment Group, wrote correctly formatted appspec.yml.
   - **Full Pipeline**: Pipeline has 3 stages Source → Build → Deploy, runs green without errors, updates ECS Service with zero downtime.

2. **API Gateway & VPC Link**
   - **VPC Link**: Successfully created VPC Link connecting to Internal ALB.
   - **API Gateway**: HTTP API operational, routes to backend, access logs to CloudWatch.

3. **ECS Services & Auto Scaling**
   - **Services**: 2 ECS Services running, Target Groups healthy, accessing Public ALB shows frontend, API returns real response.
   - **Auto Scaling**: Target tracking enabled, scales correctly when CPU exceeds threshold.

4. **CloudWatch Monitoring & Alarms**
   - **Metrics & Logs**: Container Insights, ALB Access Logs, CloudWatch Logs for ECS/API Gateway all working.
   - **Dashboard & Alarms**: Aggregated Dashboard shows real-time metrics, alarms trigger send real SNS email/SMS.

5. **Backup, Restore & Go-Live**
   - **Backup**: Automated Backup and AWS Backup Plan working, snapshot exported to S3.
   - **Restore Test**: Successfully restored temporary RDS, verified data correctness.
   - **Go-Live**: DNS points to Public ALB, system stable, monitoring tracked for first 24-48h.
