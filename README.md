<p align="center">
  <img src="https://img.shields.io/badge/AWS-Lambda-FF9900?style=for-the-badge&logo=awslambda&logoColor=white" alt="AWS Lambda"/>
  <img src="https://img.shields.io/badge/Amazon-ECR-FF9900?style=for-the-badge&logo=amazon&logoColor=white" alt="Amazon ECR"/>
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"/>
  <img src="https://img.shields.io/badge/Python-3.9-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
</p>

<h1 align="center">🚀 AIOps Lambda Docker Demo</h1>

<p align="center">
  <strong>Container Image → ECR → Lambda Deployment Demo</strong><br/>
  <em>A hands-on journey into Cloud, Serverless & AIOps</em>
</p>

<p align="center">
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-deployment">Deployment</a> •
  <a href="#-roadmap">Roadmap</a>
</p>

---

## 📖 Overview

This repository demonstrates a minimal yet production-ready example of running an **AWS Lambda function** from a **Docker container image** stored in **Amazon ECR**.

### What You'll Learn

| Concept | Description |
|---------|-------------|
| 🐳 **Containerization** | Package a Python Lambda function into a Docker image |
| 📦 **ECR Registry** | Push and manage container images in Amazon ECR |
| ⚡ **Serverless Deployment** | Update Lambda functions to use container images |
| 🔄 **CI/CD Ready** | Structure ready for GitHub Actions / GitLab CI pipelines |
| 🏗️ **IaC Prepared** | Designed for future Terraform integration |

---

## 🏗️ Architecture

```
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│                  │     │                  │     │                  │
│   Dockerfile     │────▶│   Amazon ECR     │────▶│   AWS Lambda     │
│   + app.py       │     │   Repository     │     │   Function       │
│                  │     │                  │     │                  │
└──────────────────┘     └──────────────────┘     └──────────────────┘
        BUILD                  PUSH                   DEPLOY
```

---

## 📂 Project Structure

```
aiops-lambda-docker-demo/
│
├── 🐳 Dockerfile       # Lambda container image definition
├── 🐍 app.py           # Python Lambda handler function
├── 📄 response.json    # Example test response
├── 📖 README.md        # Project documentation
└── 🚫 .gitignore       # Git ignore rules
```

---

## 🧠 Lambda Function

The heart of this demo is a simple Python handler:

```python
def handler(event, context):
    return "Docker içindeki bu kodu LAMBDA çalıştırdı!"
```

> 💡 This function is packaged into a Docker image → pushed to ECR → deployed to AWS Lambda as a container image.

---

## ✅ Prerequisites

Before you begin, ensure you have:

- [ ] **AWS Account** with appropriate permissions
- [ ] **AWS CLI** installed and configured (`aws configure`)
- [ ] **Docker** installed and running
- [ ] **IAM Permissions**:
  - ECR: `CreateRepository`, `PutImage`, `GetAuthorizationToken`
  - Lambda: `UpdateFunctionCode`

---

## 🚀 Quick Start

### 1️⃣ Build the Docker Image

```bash
docker build -t lambda-docker-demo .
```

### 2️⃣ Authenticate with ECR

```bash
aws ecr get-login-password --region eu-west-1 \
  | docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com
```

> ⚠️ Replace `<ACCOUNT_ID>` with your 12-digit AWS account ID

### 3️⃣ Tag the Image

```bash
docker tag lambda-docker-demo:latest \
  <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com/lambda-docker-demo:latest
```

### 4️⃣ Push to ECR

```bash
docker push <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com/lambda-docker-demo:latest
```

### 5️⃣ Update Lambda Function

```bash
aws lambda update-function-code \
  --function-name lambda-docker-demo \
  --image-uri <ACCOUNT_ID>.dkr.ecr.eu-west-1.amazonaws.com/lambda-docker-demo:latest
```

> ✅ Your Lambda function is now running the containerized code!

---

## 🧪 Testing

### Invoke Lambda via CLI

```bash
aws lambda invoke \
  --function-name lambda-docker-demo \
  --payload '{}' \
  response.json

cat response.json
```

### Expected Response

```json
"Docker içindeki bu kodu LAMBDA çalıştırdı!"
```

---

## 🗺️ Roadmap

### Phase 1: CI/CD Integration
- [ ] GitHub Actions workflow for automated builds
- [ ] Automatic ECR push on merge to `main`
- [ ] Lambda deployment automation

### Phase 2: Infrastructure as Code
- [ ] Terraform configuration under `/terraform`
- [ ] ECR repository provisioning
- [ ] Lambda function creation & IAM roles
- [ ] State management with S3 backend

### Phase 3: Advanced Features
- [ ] Multi-environment support (dev/staging/prod)
- [ ] AWS X-Ray tracing integration
- [ ] CloudWatch alarms & monitoring
- [ ] API Gateway integration

---

## 📚 Resources

| Resource | Link |
|----------|------|
| AWS Lambda Container Images | [Documentation](https://docs.aws.amazon.com/lambda/latest/dg/images-create.html) |
| Amazon ECR User Guide | [Documentation](https://docs.aws.amazon.com/AmazonECR/latest/userguide/) |
| Docker Best Practices | [Documentation](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) |

---

## 👤 Author

<p align="center">
  <strong>Ömer Can Gümüş</strong><br/>
  <em>AIOps • Cloud • DevOps • Serverless</em>
</p>

<p align="center">
  <a href="https://github.com/omercangumus">
    <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub"/>
  </a>
  <a href="https://linkedin.com/in/omercangumus">
    <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/>
  </a>
</p>

---

<p align="center">
  <sub>Built with ❤️ for learning Cloud & AIOps</sub>
</p>
