# Node.js CI/CD Deployment on AWS ECS Fargate

This project demonstrates a fully automated CI/CD pipeline for a containerized Node.js application using a serverless architecture.

## Architecture Overview
* **Source:** GitHub
* **Registry:** Amazon ECR (Elastic Container Registry)
* **Build:** AWS CodeBuild
* **Orchestration:** Amazon ECS (Elastic Container Service)
* **Compute:** AWS Fargate (Serverless)
* **Pipeline:** AWS CodePipeline

---

## 1. Containerization & Source
The application is a Node.js Express server. A Dockerfile is used to package the app into a standardized image.

* **Base Image:** node:18
* **Exposed Port:** 3000

> **[Insert Screenshot: Your GitHub repository file list showing Dockerfile and app.js]**

---

## 2. Automated Build (CI)
AWS CodeBuild uses a `buildspec.yml` file to automate the lifecycle of the Docker image.

**Key Build Steps:**
1. Authenticate with Amazon ECR.
2. Build the Docker image.
3. Push the image to the private ECR repository.
4. Generate an `imagedefinitions.json` artifact for the deployment stage.

> **[Insert Screenshot: AWS CodeBuild "Build history" showing a Succeeded status]**

---

## 3. Infrastructure & Orchestration
The application is hosted on **Amazon ECS** using the **AWS Fargate** launch type, removing the need to manage EC2 instances.

* **Cluster:** my-node-cluster
* **Task Definition:** Configured with 0.5 vCPU and 1 GB RAM.
* **Service:** my-node-service (Running 1 Task).
* **Security:** Inbound TCP traffic allowed on Port 3000.

> **[Insert Screenshot: Amazon ECS Console showing the Task status as RUNNING]**

---

## 4. CI/CD Pipeline (CD)
**AWS CodePipeline** automates the flow from code commit to live deployment. Any change pushed to the GitHub repository automatically triggers a new build and updates the ECS service with zero downtime.

> **[Insert Screenshot: AWS CodePipeline dashboard showing all stages in GREEN]**

---

## 5. Deployment Verification
The live application is accessible via the Public IP of the running Fargate task.

**URL Format:** `http://<Task-Public-IP>:3000`

> **[Insert Screenshot: Browser window displaying the live Node.js application]**

---

## Local Development
1. **Clone the repo:** `git clone <repo-url>`
2. **Install dependencies:** `npm install`
3. **Build image:** `docker build -t node-app .`
4. **Run container:** `docker run -p 3000:3000 node-app`
