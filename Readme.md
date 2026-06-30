☕ Coffee Website CI/CD Pipeline (DevOps Project)
🚀 Project Overview

This is a simple static website deployment project demonstrating a complete CI/CD pipeline using:

GitHub (source code management)
GitHub Actions (automation)
AWS EC2 (deployment server)
Docker (containerization)
Nginx (web server)

Whenever code is updated and pushed to GitHub, the website is automatically deployed to an EC2 instance using GitHub Actions.

🏗️ Architecture
Developer (Windows)
        ↓
GitHub (Code Repo)
        ↓
GitHub Actions (CI/CD Pipeline)
        ↓
AWS EC2 Server
        ↓
Docker Container (Nginx)
        ↓
Live Website 🌐
⚙️ Tech Stack
HTML5
Git & GitHub
GitHub Actions
AWS EC2 (Ubuntu)
Docker
Nginx
📁 Project Structure
coffee-website/
│
├── index.html
├── Dockerfile
│
├── .github/
│   └── workflows/
│       └── deploy.yml
│
└── screenshots/
    ├── 01-project-structure.png
    ├── 02-github-repo.png
    ├── 03-ec2-running.png
    ├── 04-docker-running.png
    ├── 05-live-website.png
    └── 06-github-actions-success.png
🚀 CI/CD Workflow
Developer updates website code (Windows)
Code is pushed to GitHub
GitHub Actions pipeline is triggered
EC2 server pulls latest code
Docker rebuilds the container
Old container is replaced
Updated website goes live automatically
🐳 Docker Setup
Build Docker Image
docker build -t coffee-site .
Run Container
docker run -d -p 80:80 --name coffee-container coffee-site
⚙️ GitHub Actions Workflow

This pipeline runs automatically on every push to the main branch:

name: Deploy to EC2

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Deploy via SSH to EC2
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.EC2_HOST }}
          username: ${{ secrets.EC2_USER }}
          key: ${{ secrets.EC2_SSH_KEY }}
          script: |
            cd coffee-website
            git pull origin main
            sudo docker stop coffee-container || true
            sudo docker rm coffee-container || true
            sudo docker build -t coffee-site .
            sudo docker run -d -p 80:80 --name coffee-container coffee-site
🌐 How to Run This Project
1. Clone Repository
git clone <repo-url>
cd coffee-website
2. Build Docker Image
docker build -t coffee-site .
3. Run Container
docker run -d -p 80:80 coffee-site
4. Open Website
http://<EC2_PUBLIC_IP>
🧪 CI/CD Test (Important Demo Step)

To verify pipeline works:

Step 1: Edit index.html
Step 2: Push changes
git add .
git commit -m "Updated homepage"
git push
Step 3: Wait 1–2 minutes
Step 4: Refresh browser

👉 Website updates automatically (no manual deployment needed)

📸 Screenshots
1. Project Structure

Shows local files in Windows

2. GitHub Repository

Shows code uploaded to GitHub

3. EC2 Instance Running

Shows AWS EC2 instance in running state

4. Docker Container Running

Output of:

docker ps
5. Live Website

Browser showing deployed website

6. GitHub Actions Success

Green tick showing successful pipeline execution



DevOps Learning Project — CI/CD Pipeline for Static Website Deployment