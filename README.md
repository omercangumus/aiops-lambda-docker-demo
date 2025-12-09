# AIOps Lambda Docker Demo

Container image → ECR → Lambda deployment demo for AIOps / Cloud learning.

This repository contains a minimal example of running an AWS Lambda function from a Docker container image stored in Amazon ECR.  
It is part of my journey into **Cloud, Serverless, CI/CD and AIOps**.

---

## 🔍 Overview

What this repo shows:

- Package a **Python Lambda function** into a **Docker image**
- Push that image to **Amazon ECR**
- Update an existing **AWS Lambda function** to use the new container image
- Make the project ready for future:
  - CI/CD pipelines (GitHub Actions / GitLab CI)
  - Terraform-based IaC (planned under `/terraform` later)

---

## 📂 Repository Structure

```text
aiops-lambda-docker-demo/
│
├── Dockerfile          # Docker image for Lambda
├── app.py              # Python Lambda function (handler)
├── response.json       # Example test payload/response (optional)
└── README.md

🧠 Lambda Function
def handler(event, context):
    return "Merhaba, ben Docker içinden çalışan Lambda fonksiyonuyum!"
✅ Prerequisites

AWS account

AWS CLI configured (aws configure)

Docker installed

IAM permissions:

ECR: push/pull

Lambda: UpdateFunctionCode

🐳 Build Docker Image
# In the project root
docker build -t lambda-docker-demo .

🔐 Login to ECR
aws ecr get-login-password --region eu-west-1 \
| docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com


Replace <ACCOUNT_ID> with your AWS account ID.
🏷️ Tag the Image
docker tag lambda-docker-demo:latest \
  <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com/lambda-docker-demo:latest

📦 Push Image to ECR
docker push \
  <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com/lambda-docker-demo:latest

⚡ Update Lambda to Use the New Image
aws lambda update-function-code \
  --function-name lambda-docker-demo \
  --image-uri <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com/lambda-docker-demo:latest


--function-name must match your existing Lambda function name.

After this, Lambda will run using the new Docker image.

🔄 (Planned) CI/CD & Terraform

Planned next steps for this repository:

Add a CI/CD pipeline to:

Build Docker image on each commit

Push to ECR automatically

Update the Lambda function

Add Terraform configuration under /terraform to:

Create ECR repository

Create/Update Lambda function

Manage IAM roles and permissions

👤 Author

Ömer Can Gümüş
AIOps • Cloud • DevOps • Serverless
