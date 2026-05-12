# 🚀 Automated Container Deployment Pipeline on AWS

## 📌 Project Overview

This project demonstrates a fully automated DevOps deployment pipeline using Terraform, Docker, DockerHub, GitHub Actions, and AWS EC2. The system provisions cloud infrastructure, builds a containerized application, pushes the image to DockerHub, and automatically deploys it to an EC2 instance through a CI/CD workflow.

The objective is to implement an end-to-end automated cloud deployment architecture aligned with Infrastructure as Code (IaC) and Continuous Delivery best practices.

---


## 🏗️ Architecture

Developer → GitHub Repository → GitHub Actions → DockerHub → AWS EC2 → Docker Container

### Core Technologies

- **Terraform** – Infrastructure provisioning (EC2, Security Groups)
- **Docker** – Application containerization
- **DockerHub** – Container image registry
- **GitHub Actions** – CI/CD automation
- **AWS EC2** – Cloud compute environment

---

## 📂 Project Structure

```
automated-container-deployment/
│
├── app/
│   ├── app.py
│   └── requirements.txt
│
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── terraform.tfvars
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
├── Dockerfile
├── .gitignore
└── README.md
```

---

## 🛠️ Infrastructure Provisioning (Terraform)

Terraform is used to provision:

- Ubuntu EC2 instance
- Security Group allowing:
  - Port 22 (SSH)
  - Port 80 (HTTP)
- SSH key pair association

### Steps

```
cd terraform
terraform init
terraform plan
terraform apply
```

After successful execution, Terraform outputs:

```
instance_public_ip = "xx.xx.xx.xx"
```

This confirms successful infrastructure provisioning.

---

## 🐳 Docker Containerization

The application is a Python Flask app containerized using Docker.

### Dockerfile Strategy

- Base Image: python:3.9-slim
- Install dependencies
- Copy application files
- Expose port 5000
- Run application

### Build Image Locally

```
docker build -t <docker-username>/sampleapp .
```

### Run Container Locally

```
docker run -p 80:5000 <docker-username>/sampleapp
```

The container maps:
- Internal port 5000 → Host port 80

---

## ☁️ DockerHub Integration

DockerHub stores version-controlled container images.

### Login

```
docker login
```

### Tag Image

```
docker tag sampleapp <docker-username>/sampleapp
```

### Push Image

```
docker push <docker-username>/sampleapp
```

---

## ⚙️ CI/CD Pipeline (GitHub Actions)

The workflow file is located at:

```
.github/workflows/deploy.yml
```

### Pipeline Actions

- Checkout repository
- Login to DockerHub
- Build Docker image
- Push image to DockerHub
- SSH into EC2
- Pull latest image
- Stop existing container
- Deploy updated container

The pipeline is triggered automatically on every push to the `main` branch.

---

## 🔐 Required GitHub Secrets

Go to:
Repository → Settings → Secrets and Variables → Actions

Add:

- DOCKER_USERNAME
- DOCKER_PASSWORD
- EC2_HOST
- EC2_SSH_KEY

These secrets are encrypted and prevent exposure of credentials.

---

## 🔑 SSH Setup

1. Create key pair in AWS.
2. Download `.pem` file.
3. Set permission:

```
chmod 400 automated-key.pem
```

4. Copy entire PEM file content into GitHub secret `EC2_SSH_KEY`.

---

## 🔄 Deployment Workflow

1. Developer pushes code to GitHub.
2. GitHub Actions triggers automatically.
3. Docker image is built.
4. Image is pushed to DockerHub.
5. EC2 pulls latest image.
6. Existing container is stopped and removed.
7. New container starts automatically.
8. Application becomes publicly accessible.

---

## 🌐 Access Application

After successful deployment:

```
http://<EC2_PUBLIC_IP>
```

Expected Output:

```
Automated Cloud Deployment Successful 🚀
```

---

## 🧪 Validation

Deployment success is verified by:

- Successful Terraform apply
- Docker image available in DockerHub
- GitHub Actions workflow completed successfully
- EC2 instance running container
- Public endpoint responding correctly

---

## 🔒 Security Best Practices

- No hardcoded credentials
- Encrypted GitHub Secrets
- SSH key-based authentication
- Infrastructure version-controlled
- Containerized runtime isolation

---

## ⚠️ Common Issues & Fixes

### SSH Authentication Error
- Ensure PEM key format is correct
- Ensure no extra spaces in GitHub Secret
- Confirm Security Group allows port 22

### Port Already Allocated

```
docker ps
docker stop <container_id>
docker rm <container_id>
```

---

## 🚀 Future Enhancements

- HTTPS via Let's Encrypt
- Nginx reverse proxy
- Blue-Green deployment
- AWS ECR integration
- Load Balancer
- Auto Scaling
- Kubernetes orchestration

---

## 🎯 Outcome

This project successfully demonstrates:

- Infrastructure as Code using Terraform
- Application containerization using Docker
- Automated CI/CD deployment using GitHub Actions
- Secure secret management
- Fully automated cloud deployment workflow

The system ensures automation, reproducibility, and scalability in modern cloud environments.

---

## 👤 Author

Arun 
MSc Information Systems


