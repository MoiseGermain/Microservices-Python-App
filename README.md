# 🛠️ DevOps Project: Microservices App on AWS EKS with Helm & Terraform

This project demonstrates how to build and deploy a cloud-native microservices application on **Amazon EKS** using **Helm**, **Terraform**, and secure cloud networking practices. The system converts `.mp4` videos into `.mp3` audio files and simulates a real-world, multi-service architecture with secure communication, secrets management, and infrastructure automation.

---

## 🔧 What I Built

The platform consists of four containerized microservices running in a Kubernetes cluster (EKS):

- **Auth Service** – handles user login with JWT-based authentication  
- **Converter Service** – processes `.mp4` files into `.mp3`  
- **Notification Service** – sends 2FA-enabled email alerts  
- **API Gateway** – central interface for service routing

Services communicate asynchronously via **RabbitMQ**, and data is persisted using **PostgreSQL** and **MongoDB**.

---

## 📦 Tech Stack

| Tool/Service         | Purpose                                |
|----------------------|----------------------------------------|
| **AWS EKS**          | Kubernetes orchestration               |
| **Helm**             | Kubernetes package management          |
| **Terraform**        | Infrastructure provisioning (EKS, VPC) |
| **RabbitMQ**         | Asynchronous message queueing          |
| **PostgreSQL/MongoDB** | Persistent data layers               |
| **IAM, Secrets, JWT**| Security and access control            |
| **ALB, Route 53**    | Ingress routing and DNS                |
| **GitHub Actions**   | CI/CD and automation pipelines         |

---

## ⚙️ Key Features

- 🔐 **Secure authentication** with JWT tokens and IAM roles  
- 🔁 **Message-driven architecture** using RabbitMQ  
- 🛡️ **Secrets managed via Kubernetes and IAM**  
- 🔧 **Infrastructure as Code (IaC)** with Terraform for EKS, VPC, subnets, ALB, and IAM policies  
- 📡 **Ingress control** with AWS ALB and Route 53 DNS routing  
- ☁️ **Multi-AZ EKS cluster deployment** with security groups and network policies  
- 🔄 **CI/CD pipeline** using GitHub Actions for automated builds and Helm-based deployments  

---

## 🚀 Deployment Overview

1. Provisioned AWS infrastructure using **Terraform**:  
   - VPC with public/private subnets  
   - Internet Gateway, NAT Gateway, and Route Tables  
   - EKS cluster and node groups with IAM roles  
   - ALB, Route 53, and IAM policies for service access

2. Deployed microservices using **Helm** and Kubernetes manifests  
3. Secured workloads with **Kubernetes Secrets** and environment isolation  
4. Configured **RabbitMQ queues** for `mp3` and `video` processing  
5. Tested service APIs for login, upload, and download workflows

---

## 🧠 Security Highlights

- **IAM role scoping** for least privilege access  
- **TLS-based authentication** between services  
- **2FA email authentication** using secure Gmail credentials stored in K8s secrets  
- **Ingress/egress managed via ALB, security groups, and private subnets**  
- **No hardcoded credentials** – all secrets managed via `secret.yaml` and AWS IAM

---

## 📈 What I Learned

- Built a production-style, multi-service system on **AWS EKS** with automated, version-controlled deployments  
- Gained experience with **Helm**, **Terraform**, and **Kubernetes control plane concepts**  
- Practiced **PCI-style security**: IAM enforcement, isolated networks, secrets, and encryption  
- Strengthened my ability to **troubleshoot cloud-native deployments** in a distributed environment

---

## 🧼 Clean Teardown

To avoid unnecessary AWS charges, I removed all cloud resources after testing:

- Deleted EKS node group and cluster via AWS Console  
- Destroyed VPC, ALB, and associated Terraform resources

---

## 🙌 Clone or Fork This Repo

If you're learning **Terraform, EKS, or Helm**, or just want a clean, working example of a real-world cloud-native app, feel free to clone or fork this repo.

Questions? Let's connect on [LinkedIn](https://linkedin.com/in/moisegermain)
