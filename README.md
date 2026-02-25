
# 🚀 CI-CD-NodeJS-App

## 📌 Project Overview

This repository contains a complete **CI/CD automation pipeline** for deploying a Node.js application using **GitHub Actions**, **Docker**, and **AWS EC2**.

The project demonstrates essential DevOps principles including:

- Automated build and deployment workflow  
- Docker containerization  
- Continuous Integration via GitHub Actions  
- Continuous Deployment to AWS EC2  
- Automatic health checks after deployment  

This repository represents a real-world, fully automated DevOps pipeline.

---

## 🎯 Project Objectives

- Automate the build and deployment of a Node.js application  
- Containerize the application using Docker  
- Automatically push Docker images to Docker Hub  
- Deploy new versions on an EC2 instance once code is pushed to `main`  
- Maintain a clean and simple CI/CD workflow  
- Apply fast, idempotent, and reliable deployment practices  

---

## 🛠 Technologies Used

- **Node.js / Express**
- **Docker**
- **GitHub Actions**
- **AWS EC2**
- **SSH Authentication**
- **Linux (Ubuntu / Amazon Linux)**

---

## 📂 Project Structure

```
CI-CD-NodeJS-App/
│
├── app.js                  # Main Node.js application
├── package.json            # Dependencies & app metadata
├── Dockerfile              # Docker image definition
├── README.md               # Project documentation
├── 2024_1.png
├── Screenshot (107).png
├── Screenshot (108).png
├── Screenshot (109).png
│
└── .github/
    └── workflows/
        └── push-up.yaml    # CI/CD pipeline definition
```

---

## ⚙️ Application Code (Node.js)

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello, Abdallah, Welcome to you in DevOpe Era!');
});

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

---

## 🐳 Docker Containerization

Docker is used to package the application in a portable, reproducible container image.

### Dockerfile

```dockerfile
FROM node:16

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

### Build Docker Image

```bash
docker build -t nodejs-app .
```

### Run the Container

```bash
docker run -p 3000:3000 nodejs-app
```

---

## 🚦 CI/CD Pipeline (GitHub Actions)

The CI/CD pipeline is implemented in:

```
.github/workflows/push-up.yaml
```

### 🔁 Triggered On:

- Push to `main`  
- Pull Requests targeting `main`

### 🔧 Pipeline Steps:

- Checkout repository  
- Set up Docker Buildx  
- Authenticate to Docker Hub  
- Build Docker image  
- Push image to Docker Hub (for pushes to main)  
- SSH into AWS EC2  
- Pull latest image  
- Stop old container (if exists)  
- Start new container mapped to `${DEPLOY_PORT}`  
- Apply Docker health checks  
- Clean up old Docker images  

---

## 🔐 Required GitHub Secrets

Add these under:

**Settings → Secrets and variables → Actions**

| Secret Name        | Description                 |
|-------------------|-----------------------------|
| DOCKER_USERNAME   | Docker Hub username         |
| DOCKER_PASSWORD   | Docker Hub password/token   |
| AWS_SSH_KEY       | Private SSH key for EC2     |
| AWS_HOST          | EC2 public IP/DNS           |
| DEPLOY_PORT       | Port exposed on EC2 server  |

---

## 🧪 Running the Application Locally

Install dependencies:

```bash
npm install
```

Start the server:

```bash
npm start
```

Visit:

```
http://localhost:3000
```

---

## 🌐 Deployment Architecture

```
        ↓
GitHub Actions CI/CD Pipeline
        ↓
Docker Image Build
        ↓
Push Image to Docker Hub
        ↓
SSH into AWS EC2
        ↓
Pull Latest Image
        ↓
Stop Old Container
        ↓
Start New Container
        ↓
Health Check
```

---

## 🎯 Summary

This project demonstrates a complete, real-world CI/CD pipeline using **GitHub Actions**, **Docker**, and **AWS EC2**.
The pipeline builds, ships, deploys, and verifies the application automatically—making it an efficient and fully automated DevOps workflow.

