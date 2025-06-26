# 🧱 Terraform Infrastructure – AWS EKS Microservices Project

This directory contains the Terraform code used to provision the AWS infrastructure for the microservices-based application deployed on Amazon EKS.

---

## 📁 Directory Structure

```bash
terraform/
├── main.tf         # Root module: VPC, EKS, IAM, networking
├── variables.tf    # Input variables
├── outputs.tf      # Output values
├── eks/            # EKS module (cluster, node groups)
├── vpc/            # VPC module (subnets, NAT, IGW, routes)
├── iam/            # IAM roles and policies
├── alb/            # Application Load Balancer config



---

## 🚀 What This Terraform Setup Provisions

- **VPC** with public/private subnets across multiple availability zones
- **Internet Gateway & NAT Gateway** for outbound access
- **EKS Cluster** with managed node groups
- **IAM roles** for EKS, node group, and service access
- **Application Load Balancer (ALB)** for ingress traffic to Kubernetes
- **Route 53 DNS records** (optional)
- Security groups for cluster communication

---

## ✅ Prerequisites

Make sure you have the following installed:

- [Terraform](https://www.terraform.io/downloads)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- An AWS account and IAM user with sufficient permissions
- `kubectl` and `aws-iam-authenticator` installed and configured

---

## 🔧 Usage

### 1. Initialize Terraform

```bash
cd terraform/
terraform init

2. Plan Infrastructure
terraform plan -out=tfplan

3. Apply Infrastructure
terraform apply tfplan

---

📝 Input Variables
Define your inputs in a terraform.tfvars file or pass them inline:
region           = "us-east-1"
cluster_name     = "eks-microservices"
vpc_cidr         = "10.0.0.0/16"
public_subnets   = ["10.0.1.0/24", "10.0.2.0/24"]
private_subnets  = ["10.0.3.0/24", "10.0.4.0/24"]
desired_capacity = 2
instance_type    = "t3.medium"

---

🔐 Security Considerations
IAM roles follow the principle of least privilege

Kubernetes secrets are used for application credentials

Private subnets are used for worker nodes to reduce surface exposure

ALB listens on HTTPS (port 443) and routes to services through Ingress controller

---

📤 Outputs
After deployment, Terraform will return values such as:

cluster_endpoint – EKS API endpoint

cluster_name – Name of your EKS cluster

alb_dns_name – DNS name for the Application Load Balancer

kubeconfig – Data to populate your ~/.kube/config

---

🧼 Clean-Up
To destroy all infrastructure when you're done:
terraform destroy

---

📚 Learn More
Terraform AWS Provider Docs

Amazon EKS Architecture

AWS ALB Ingress Controller

Questions or suggestions? Reach out on LinkedIn

Let me know if you want me to help you version this for a multi-environment setup (`dev`, `prod`, `shared`) or modularize the VPC, EKS, and ALB layers.


