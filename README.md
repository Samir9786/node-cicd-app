**🚀 CI/CD Pipeline with Jenkins, Docker & Node.js on AWS EC2**

This project demonstrates a complete CI/CD pipeline using Jenkins to automate the build and deployment of a Node.js application inside a Docker container on an AWS EC2 Ubuntu server.
It simulates a real DevOps workflow used in production environments.

**📌 Architecture**

GitHub → Jenkins → Docker → EC2 Deployment
Source Code stored in GitHub
Jenkins pulls code and runs pipeline
Docker builds application image
Container runs on EC2

**🛠 Tech Stack**

Node.js
Docker
Jenkins
AWS EC2 (Ubuntu 22.04)
Git & GitHub

**📂 Project Structure**

node-cicd-app/
│
├── app.js
├── package.json
├── Dockerfile
└── README.md

**⚙️ Application Overview**

A simple Node.js HTTP server that returns:
CI/CD Pipeline Working!
Runs on port 3000 inside Docker container.

**🐳 Docker Configuration**

Dockerfile:
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]

**🔄 Jenkins Pipeline Script**

pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/node-cicd-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t node-app .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker stop node-container || true'
                    sh 'docker rm node-container || true'
                    sh 'docker run -d -p 80:3000 --name node-container node-app'
                }
            }
        }
    }
}

**🚀 How to Run This Project**

1️⃣ Launch EC2 Instance
Ubuntu 22.04
Open ports:
22 (SSH)
8080 (Jenkins)
80 (App)

2️⃣ Install Required Tools on EC2
Java (OpenJDK 17)
Jenkins
Docker

3️⃣ Configure Jenkins
Install suggested plugins
Create Pipeline job
Add pipeline script
Click Build Now

🌐 Access the Application
After successful build:
http://your-ec2-public-ip
You should see:
CI/CD Pipeline Working!

**🔥 What This Project Demonstrates**

CI/CD fundamentals
Jenkins Pipeline as Code
Docker image build automation
Automated deployment on EC2
DevOps workflow integration
