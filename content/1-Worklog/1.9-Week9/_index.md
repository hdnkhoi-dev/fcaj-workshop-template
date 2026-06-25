---
title: "Week 9 Worklog"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
### Week 9 Objectives:

* Develop GlobalMart Website (Frontend: Vite/React, Backend: Java Spring Boot, Database: MySQL RDS).
* Configure CI/CD and Containerization for Frontend & Backend with Dockerfile, buildspec.yml, appspec.yml, taskdef.json.
* Design and configure Terraform modules for the entire AWS infrastructure.

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
            Develop GlobalMart Website
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
            Develop GlobalMart Website
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
            Develop GlobalMart Website
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
            Configure CI/CD and Containerization (Frontend & Backend)
            <ul>
              <li>Write optimized Dockerfile to build images for Frontend and Backend</li>
              <li>Configure buildspec.yml for AWS CodeBuild automation</li>
              <li>Set up appspec.yml and taskdef.json for Blue/Green deployment on Amazon ECS Fargate</li>
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
            Design and configure Terraform modules
            <ul>
              <li>Build Terraform project structure with separate modules</li>
              <li>Create modules: vpc, iam, ecr, ecs, rds, s3, codepipeline, monitoring, backup</li>
              <li>Configure main.tf, variables.tf, outputs.tf for the entire project</li>
              <li>Add configuration files (appspec.yml, buildspec.yml, taskdef.json) to the project</li>
              <li>Set up terraform.tfvars.example and .gitignore files</li>
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


### WEEK 9 ACHIEVEMENTS: WEBSITE CODE, CI/CD & TERRAFORM

1. **Develop GlobalMart Website**
   - **Frontend**: Implemented Frontend using Vite/React, Tailwind CSS.
   - **Backend**: Built Backend with Java Spring Boot.
   - **Database**: Designed connection to MySQL RDS.

2. **Configure CI/CD and Containerization**
   - **Dockerfile**: Wrote optimized Dockerfile to build Frontend and Backend images.
   - **buildspec.yml**: Configured buildspec.yml for AWS CodeBuild.
   - **appspec.yml & taskdef.json**: Set up files to support Blue/Green deployment on Amazon ECS Fargate.

3. **Terraform design and configuration**
   - **Project structure**: Successfully built Terraform structure with separate modules (vpc, iam, ecr, ecs, rds, s3, codepipeline, monitoring, backup).
   - **Configuration files**: Created and configured main.tf, variables.tf, outputs.tf.
   - **State management**: Set up .gitignore and terraform.tfvars.example to safely manage state files and environment variables.
