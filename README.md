# 🛠️ DevOps Project: Microservices Python App (Video to Audio Converter)

This project helped me gain hands-on experience deploying a microservices-based application on AWS using Kubernetes. It’s a Python-based system that converts `.mp4` videos into `.mp3` audio files. The app is built using four microservices running in containers, all deployed and managed on **Amazon EKS (Elastic Kubernetes Service)**.

---

## 🔧 What I Built

This project is made up of the following services:

- **auth-server** – handles user login and JWT authentication
- **converter-module** – picks up `.mp4` files and converts them into `.mp3`
- **notification-server** – sends email notifications with two-factor auth
- **gateway-server** – acts as the API gateway between users and services

I used **RabbitMQ** to pass messages between services, and **PostgreSQL** and **MongoDB** for data storage.

---

## 🚀 Why I Built This

I wanted to:
- Learn how to deploy and manage **containerized microservices** at scale
- Work with **AWS EKS**, **Helm**, and **Kubernetes manifests**
- Practice securing cloud-native applications using **IAM**, **JWT**, and **Kubernetes secrets**
- Gain experience with messaging systems like **RabbitMQ** and database integration in cloud workloads

---

## 🧱 Tools & Services I Used

| Tool | Purpose |
|------|---------|
| **AWS EKS** | Kubernetes hosting |
| **Helm** | Service deployment |
| **kubectl** | Cluster management |
| **Python** | Service logic |
| **RabbitMQ** | Message queueing |
| **PostgreSQL / MongoDB** | Persistent data storage |
| **IAM, Secrets, JWT** | Security & access control |

---

## ⚙️ How I Deployed It (High-Level Flow)

1. **Set up PostgreSQL and MongoDB** for application persistence  
2. **Deployed RabbitMQ** for task queuing between microservices  
3. Created `mp3` and `video` queues in RabbitMQ  
4. Deployed each service (`auth`, `converter`, `gateway`, `notification`) using **Helm charts** and **Kubernetes manifests**  
5. Verified everything was working using:
   ```bash
   kubectl get all

## 📦 How I Built the EKS Cluster

To create the EKS cluster from scratch, I followed these key steps:

- Created IAM roles for the EKS cluster and EKS node group  
- Created the EKS cluster via AWS Console  
- Configured security groups with inbound rules for services  
- Enabled the EBS CSI Addon for persistent volume support  
- Connected to the cluster using the AWS CLI:

```bash
aws eks update-kubeconfig --name <cluster_name> --region <region>
```

## 📡 API Overview
Once deployed, I tested the system using these endpoints:

🔐 Login
```
POST http://<nodeIP>:30002/login
```
Logs in a user using basic authentication and returns a JWT token.

## 📤 Upload a Video
```
POST http://<nodeIP>:30002/upload
```
Uploads an .mp4 video file and initiates the conversion process.

## 📥 Download the Audio
```
GET http://<nodeIP>:30002/download?fid=<file_id>
```
Downloads the converted .mp3 file using the file identifier.

## 🔒 Email Notifications & 2FA

To enable email-based 2FA for this application, I followed these steps:

1. I generated an **app-specific password** from my Gmail account under the "Security" settings  
2. I stored this password securely in the Kubernetes `secret.yaml` file under the `notification-server` microservice  
3. This allowed the app to authenticate with Gmail and send **2FA verification emails** to users during login

All sensitive credentials were handled securely using Kubernetes Secrets to avoid hardcoding any sensitive data into the manifests or application code.

## 🧼 How I Destroyed the Infrastructure

Once testing was complete, I cleaned up all the cloud resources to avoid ongoing AWS charges:

1. I deleted the **EKS Node Group** from the AWS Console  
2. Then I deleted the **EKS Cluster** itself  

This ensured that no compute, networking, or storage resources remained active after the project was completed.

## ✅ What I Learned

Throughout this project, I gained practical experience in:

- Building and deploying **multi-service applications** on AWS using Kubernetes  
- Using **Helm**, `kubectl`, and managing **IAM roles and AWS networking** for secure infrastructure  
- Understanding the power of **microservices and asynchronous communication** via RabbitMQ  
- Securing cloud-native applications with **JWT**, **Kubernetes Secrets**, and **IAM-based access control**

---

### 🧠 Reflections & Challenges Overcome

- **Service discovery in EKS:** Initially struggled with getting services to communicate across pods. I learned to define proper `ClusterIP` services and DNS-based service discovery in Kubernetes.
- **RabbitMQ queue initialization:** Had to manually configure queues before deployment, which led me to explore automating that as part of CI/CD or Helm post-install hooks.
- **Persistent storage for databases:** Setting up volume claims using the EBS CSI driver was new territory. I overcame issues by enabling the add-on and correctly configuring storage classes.
- **Email & 2FA integration:** Handling Gmail authentication securely in a containerized environment taught me the importance of managing secrets properly, and how to structure manifests without exposing credentials.

These challenges made the project both rewarding and educational, giving me insight into real-world DevOps workflows and multi-service deployments at scale.

## 🙌 Feel Free to Fork or Clone This Repo

If you're exploring **Kubernetes**, **Amazon EKS**, or working with **multi-container applications**, this project is a great hands-on starting point.

Want help replicating it or adapting it to your use case?  
Feel free to reach out to me on [LinkedIn](https://linkedin.com/in/moisegermain) — I’d be happy to connect!
