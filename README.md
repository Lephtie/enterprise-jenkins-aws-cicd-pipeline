# enterprise-jenkins-aws-cicd-pipeline
Developer → GitHub → CI Pipeline → Container Registry → Deployment

# Overview
An enterprise-grade CI/CD pipeline that uses Jenkins and Groovy to automate Java application builds with Maven, enforce code quality via Checkstyle and SonarQube, containerize applications with Docker, push images to AWS ECR, and deploy to AWS ECS.

# Technology Stack
- *CI/CD:* Jenkins (Declarative Pipeline, Groovy) 
- *Build Tool:* Maven 3.9
- *Language:* Java (JDK 17/21)
- *Code Quality:* Checkstyle, SonarQube
- *Containerization:* Docker (Multi-stage build)
- *Container Registry:* AWS Elastic Container Registry (ECR)
- *Deployment Platform:* AWS Elastic Container Service (ECS)
- *Cloud Service Provider:* AWS
- *Source Control:* GitHub

# Prerequisites
Jenkins installed with required plugins:
- Docker Pipeline
- AWS ECR Plugin
- SonarQube Scanner
- ECS Plugin
- Maven and JDK configured in Jenkins Global Tools
- AWS CLI installed and configured on Jenkins server
- AWS credentials stored securely in Jenkins Credentials Manager
- Existing AWS ECS cluster and service
- Docker Engine installed on Jenkins server
- SonarQube server configured in Jenkins

# Pipeline Workflow
1. **Source Code Checkout**
- Fetches application source code from GitHub.

2. **Build & Package**
- Builds the Java application using Maven.
- Generates WAR artifacts.
- Skips tests during build for faster execution.

3. **Static Code Analysis**
- Performs Checkstyle analysis to enforce coding standards.
- Runs SonarQube analysis to measure code quality, bugs, and technical debt.

4. **Docker Image Build**
- Builds a Docker image using a multi-stage Dockerfile.
- Tags images using Jenkins build number and `latest`.

5. **Push Image to AWS ECR**
- Authenticates with AWS ECR using Jenkins credentials.
- Pushes versioned and latest Docker images.

6. **Cleanup**
- Removes local Docker images to free Jenkins server disk space.

7. **Deploy to AWS ECS**
- Triggers a new ECS service deployment.
- Forces ECS to pull the latest image from ECR.

# Key Features
- Fully automated CI/CD pipeline
- Integrated static code analysis and quality gates
- Secure Docker image management using AWS ECR
- Automated deployment to AWS ECS
- Scalable and production-ready DevOps workflow
