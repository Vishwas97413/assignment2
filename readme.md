# Dockerized Microservice Deployment on AWS ECS with CI/CD using GitHub Actions

## Project Overview

This project demonstrates how a simple Python microservice application was containerized using Docker, pushed to GitHub, deployed on AWS ECS using ECR, and automated using GitHub Actions CI/CD pipeline.

The project also includes monitoring integration planning using AWS CloudWatch, Prometheus, and Grafana for microservice monitoring.

## The complete workflow includes:

- Creating a simple Python application
- Containerizing the application using Docker
- Building and testing Docker image locally
- Initializing Git and pushing code to GitHub
- Creating SSH authentication for GitHub
- Creating AWS ECR repository
- Pushing Docker image to ECR
- Creating ECS Cluster, Task Definition, and Service
- Deploying containerized application on ECS
- Automating deployment using GitHub Actions CI/CD pipeline
- Monitoring setup using CloudWatch / Prometheus / Grafana

## Technologies Used

- Python
- Docker
- Git & GitHub
- AWS ECS
- AWS ECR
- GitHub Actions
- AWS CloudWatch
- Prometheus
- Grafana

## Project Architecture

Developer Code Changes
        ↓
GitHub Repository
        ↓
GitHub Actions Pipeline
        ↓
Docker Image Build
        ↓
Push Image to AWS ECR
        ↓
AWS ECS Task Revision
        ↓
Force New Deployment
        ↓
Application Running on ECS
        ↓
Monitoring using CloudWatch / Prometheus / Grafana

### Step 1 — Creating Simple Python Application

- app.py created, this file contains the Python Flask application.
- requirements.txt created, this file contains Python dependencies.
- Dockerfile created, this file is used to create Docker image.

### Step 2 — Building Docker Image

** Commands Used **

- Build Docker Image
 docker build -t helloapp .
- Check Docker Images
 docker images
- Run Docker Container
 docker run -d -p 5000:5000 helloapp
- Check Running Containers
 docker ps

### Step 3 — Initializing Git Repository
** Commands Used **
- Initialize Git
 git init
- Add Files to Git
 git add .
- Commit Files
 git commit -m "Initial commit"


### Step 4 — Connecting GitHub using SSH Key
- Generate SSH Key
 ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
- Start SSH Agent
 eval "$(ssh-agent -s)"
- Add SSH Key
 ssh-add ~/.ssh/id_rsa
- View Public Key
cat ~/.ssh/id_rsa.pub
- Add GitHub Remote Repository
git remote add origin git@github.com:Vishwas97413/assignment2.git
- Push Code to GitHub
 git push -u origin main

### Step 5 — Creating AWS ECR Repository

** Purpose **
Amazon ECR (Elastic Container Registry) is used to store Docker images.

** Steps Performed **
- Open AWS Console
- Navigate to ECR
- Create Repository
- Repository name: flask-app
- Login to ECR from Linux Machine
  (aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <account-id>.dkr.ecr.ap-south-1.amazonaws.com)
- Tag Docker Image
  (docker tag flask-app:latest <account-id>.dkr.ecr.ap-south-1.amazonaws.com/flask-app:latest)
- Push Image to ECR
  docker push <account-id>.dkr.ecr.ap-south-1.amazonaws.com/flask-app:latest

### Step 6 — Creating ECS Cluster

**Purpose **
Amazon ECS is used to run Docker containers in AWS.

** Steps Performed **
- Open ECS Console
- Create Cluster
- Select Fargate only
- Provide Cluster Name
- Create Cluster

### Step 7 — Creating ECS Task Definition

** Purpose **
Task Definition acts as blueprint for container deployment.

** Steps Performed **
- Create Task Definition
- Select Fargate
- Add Container Details
- Add ECR Image URI
- Configure CPU and Memory
- Configure Port Mapping
- Save Task Definition

### Step 8 — Creating ECS Service

** Purpose **
ECS Service maintains running containers continuously.

** Steps Performed **
- Open ECS Cluster
- Create Service
- Select Task Definition
- Choose Number of Tasks
- Configure Networking
- Deploy Service

### Step 9 — Running ECS Task

Application container successfully started inside ECS.
The application was accessible through ECS public IP.

### Step 10 — Automating Deployment using GitHub Actions

GitHub Actions automates Docker build and ECR push whenever code is pushed to GitHub. This removes manual deployment effort.

created GitHub Actions Workflow File
.github/workflows/deploy.yml


### Inside GitHub Repository added Secrets

Settings → Secrets and Variables → Actions

Added:

AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
ECS_SERVICE_NAME
ECS_CLUSTER_NAME
ECR_REPOSITORY_NAME
AWS_REGION

** CI/CD Workflow Process **

Code Push to GitHub
        ↓
GitHub Actions Triggered
        ↓
Docker Image Build
        ↓
Push Image to AWS ECR
        ↓
Create ECS Task Revision
        ↓
Force New ECS Deployment
        ↓
Updated Application Running

** ECS Task Revision and Force Deployment **

- After New Docker Image Push, Create New Task Revision.
- Inside ECS Service: Service → Update Service → Force New Deployment

### Step 11 — Monitoring using CloudWatch, Prometheus, and Grafana

** CloudWatch is used for: **

ECS Logs Monitoring, CPU Usage Monitoring, Memory Usage Monitoring, Container Health Monitoring, CloudWatch Logs, Alarms and Monitoring

** Prometheus **

Prometheus collects metrics from microservices. Used for Application Metrics, Container Metrics, ECS Metrics Collection

** Grafana **

Grafana visualizes monitoring metrics using dashboards. Used for CPU Monitoring Dashboard, Memory Monitoring Dashboard, ECS Health Dashboard, Container Performance Visualization, Key Learning Outcomes

## Through this project, I learned:

- Docker containerization
- Docker image creation
- Git and GitHub workflow
- SSH authentication setup
- AWS ECR image management
- ECS container orchestration
- CI/CD automation using GitHub Actions
- Cloud deployment concepts
- Monitoring using CloudWatch, Prometheus, and Grafana

## Conclusion

This project successfully implemented a complete DevOps workflow for deploying a containerized microservice application on AWS ECS. The project automated the software deployment lifecycle using GitHub Actions CI/CD pipeline and integrated monitoring tools like CloudWatch, Prometheus, and Grafana for observability and performance monitoring. The implementation reduced manual deployment effort and demonstrated modern cloud-native deployment practices used in real-world industry environments.
