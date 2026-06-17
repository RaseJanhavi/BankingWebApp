# 🏦 BankingWebApp — CI/CD Pipeline with Jenkins, Docker & Kubernetes

A Java-based Banking Web Application deployed through a fully automated CI/CD pipeline using Jenkins, Maven, Docker, and Kubernetes.

---

## 📌 Project Overview

This project demonstrates an end-to-end DevOps pipeline for a Java banking application — from source code checkout to live deployment on a Kubernetes cluster. Every commit to the repository automatically triggers the full build, containerization, and deployment workflow.

---

## 🏗️ Pipeline Architecture


GitHub Repo
    │
    ▼
Jenkins (SCM Checkout)
    │
    ▼
Maven Build → JAR Package
    │
    ▼
Docker Image Build & Tag
    │
    ▼
Push to DockerHub Registry
    │
    ▼
Kubernetes Deployment (kubectl apply)
    │
    ▼
Application Live via NodePort Service


## ⚙️ Pipeline Stages

| Stage | Tool | Description |
|-------|------|-------------|
| SCM Checkout | Jenkins + Git | Pulls latest source code from GitHub on every commit |
| Application Build | Maven | Compiles source code and packages it as a deployable JAR |
| Docker Image Build | Docker | Builds and tags versioned Docker image (`BUILD_NUMBER` + `latest`) |
| Registry Login | DockerHub | Authenticates securely using Jenkins credentials |
| Image Publish | DockerHub | Pushes both versioned and latest image to DockerHub |
| Deploy to Kubernetes | kubectl + SSH | Applies Kubernetes YAML manifests on the cluster via SSH publisher |

---

## 🛠️ Tech Stack

- **Application:** Java (Spring Boot)
- **Build Tool:** Maven
- **CI/CD:** Jenkins (Declarative Pipeline)
- **Containerization:** Docker
- **Container Registry:** DockerHub
- **Orchestration:** Kubernetes
- **Deployment Config:** Kubernetes Deployment + NodePort Service YAML

---

## 📂 Repository Structure

BankingWebApp/
├── src/                      # Java application source code
├── Dockerfile                # Multi-stage Docker build configuration
├── Jenkins_file              # Declarative Jenkins pipeline definition
├── bankingdeploy.yaml        # Kubernetes Deployment & Service manifest
├── pom.xml                   # Maven project configuration
└── .mvn/                     # Maven wrapper files



## 🚀 How to Run

### Prerequisites
- Jenkins server with a configured slave node (`slave1`)
- Docker installed on Jenkins agent
- DockerHub credentials configured in Jenkins (`dockerloginid`)
- Kubernetes cluster accessible via SSH (configured as `Kubernetes_Master` in Jenkins)

### Steps

**1. Clone the repository**
bash
git clone https://github.com/RaseJanhavi/BankingWebApp.git
cd BankingWebApp


**2. Configure Jenkins**
- Add DockerHub credentials in Jenkins with ID `dockerloginid`
- Configure SSH server for Kubernetes master in Jenkins → Manage Jenkins → Configure System
- Create a new Pipeline job and point it to this repository's `Jenkins_file`

**3. Trigger the Pipeline**
- Push any commit to the `master` branch
- Jenkins automatically runs all pipeline stages

**4. Verify Deployment**
bash
kubectl get pods
kubectl get svc

Access the application via the NodePort exposed by the Kubernetes service.

---

## 🔑 Key DevOps Concepts Demonstrated

- **Infrastructure as Code** — Kubernetes manifests define the desired deployment state
- **Immutable Deployments** — Every build produces a uniquely tagged Docker image
- **Automated Release Pipeline** — Zero manual steps from commit to deployment
- **Credential Management** — DockerHub secrets managed securely via Jenkins credentials store
- **Container Orchestration** — Kubernetes manages pod lifecycle, scaling, and service exposure

---

## 📸 DockerHub Image

docker pull janhavi225/bankingwebapp:latest




## 👩‍💻 Author

**Janhavi Rase**
[![LinkedIn](https://img.shields.io/badge/LinkedIn-janhavi--rase-0077B5?style=flat&logo=linkedin)](https://linkedin.com/in/janhavi-rase)
[![GitHub](https://img.shields.io/badge/GitHub-RaseJanhavi-181717?style=flat&logo=github)](https://github.com/RaseJanhavi)
