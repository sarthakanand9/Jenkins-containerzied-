🚀 Jenkins CI/CD Pipeline for Dockerized Flask Application

This project demonstrates a complete CI/CD pipeline using Jenkins, Docker, Docker Compose, and GitHub on an AWS EC2 Ubuntu server.

Whenever code is pushed to GitHub, Jenkins can pull the latest source code, build the Docker image, and deploy the application automatically using Docker Compose.

🏗️ Tech Stack
Jenkins
Docker
Docker Compose
Python Flask
MySQL 5.7
Git & GitHub
Ubuntu 24.04 (AWS EC2)
📁 Project Structure
.
├── app.py
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── templates/
│   └── index.html
└── README.md
⚙️ One-Time Server Setup

Install the required software on the Jenkins server.

Update Server
sudo apt update
sudo apt upgrade -y
Install Git
sudo apt install git -y
Install Docker
sudo apt install docker.io -y
Enable Docker
sudo systemctl enable docker
sudo systemctl start docker
Install Docker Compose
sudo apt install docker-compose-v2 -y
Allow Jenkins to Access Docker
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
🔧 Jenkins Configuration
Source Code Management

Repository:

https://github.com/<your-username>/<repository-name>.git

Branch:

*/main
🖥️ Jenkins Execute Shell Script
#!/bin/bash
set -e

echo "===== Starting Deployment ====="

cd "$WORKSPACE"

echo "Workspace:"
pwd

echo "Listing Files:"
ls -la

docker compose down || true

docker compose build

docker compose up -d

echo "Waiting for application..."
sleep 20

docker ps

docker compose ps

docker compose logs --tail=20

curl http://localhost:5000

echo "Deployment Successful!"
🚀 Deployment Workflow
Developer
      │
      ▼
Push Code to GitHub
      │
      ▼
Jenkins Build Trigger
      │
      ▼
Clone Latest Repository
      │
      ▼
Build Docker Image
      │
      ▼
Start Docker Containers
      │
      ▼
Flask Connects to MySQL
      │
      ▼
Health Check
      │
      ▼
Deployment Successful
🐳 Docker Services
Flask Application
Built from Dockerfile
Exposed on Port 5000
MySQL Database
Image: mysql:5.7
Database: userdb
Table: users
External Port: 3307
📊 Verify Running Containers
docker ps
📄 View Container Logs
docker compose logs
🛑 Stop Application
docker compose down
🔄 Rebuild Application
docker compose up --build
🗄️ Verify Database Records

Access MySQL:

docker exec -it <mysql_container_name> mysql -u root -p

Password:

root

Use Database:

USE userdb;

View Records:

SELECT * FROM users;
🌐 Application URL
http://<EC2-Public-IP>:5000

Example:

http://54.242.234.214:5000
📌 Features
Automated deployment using Jenkins
Dockerized Flask application
MySQL database container
Docker Compose orchestration
Automatic image build on each deployment
Health check using curl
Centralized container logging
Easy rollback by redeploying a previous build
📚 Learning Outcomes

Through this project, I gained hands-on experience with:

Jenkins Freestyle Jobs
CI/CD pipeline implementation
GitHub integration with Jenkins
Docker image creation
Docker Compose orchestration
Flask and MySQL containerization
AWS EC2 server provisioning
Linux administration
Automated application deployment
Container monitoring and troubleshooting
