In this DevOps task, you need to build and deploy a full-stack CRUD application using the MEAN stack (MongoDB, Express, Angular 15, and Node.js). The backend will be developed with Node.js and Express to provide REST APIs, connecting to a MongoDB database. The frontend will be an Angular application utilizing HTTPClient for communication.  

The application will manage a collection of tutorials, where each tutorial includes an ID, title, description, and published status. Users will be able to create, retrieve, update, and delete tutorials. Additionally, a search box will allow users to find tutorials by title.

## Project setup

### Node.js Server

cd backend

npm install

You can update the MongoDB credentials by modifying the `db.config.js` file located in `app/config/`.

Run `node server.js`

### Angular Client

cd frontend

npm install

Run `ng serve --port 8081`

You can modify the `src/app/services/tutorial.service.ts` file to adjust how the frontend interacts with the backend.

Technology Stack

Frontend: Angular 15
Backend: Node.js with Express
Database: MongoDB
Containerization: Docker
Orchestration: Docker Compose
CI/CD: GitHub Actions
Cloud Provider: AWS EC2 (Ubuntu)
Reverse Proxy: Nginx

Docker Setup

Backend Dockerfile:

Uses node:18 base image

Installs dependencies

Exposes port 5000

Runs the application using npm start

Frontend Dockerfile:

Uses multi-stage build

Builds Angular production bundle

Serves static files using Nginx

Docker images:

shekhar2298/dd-backend:latest
shekhar2298/dd-frontend:latest

Docker Compose services:

MongoDB

Backend

Frontend

Cloud Deployment on AWS EC2

EC2 Configuration:

Ubuntu server

Port 22 open for SSH

Port 80 open for HTTP

Docker installation:

curl -fsSL https://get.docker.com
 -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu

Clone repository:

git clone https://github.com/Shekhar2298/dd-mean-devops.git

cd dd-mean-devops

Start application:

docker compose up -d

CI/CD Pipeline

The pipeline is triggered on every push to the main branch.

Steps performed:

Checkout repository

Login to Docker Hub

Build backend Docker image

Build frontend Docker image

Push images to Docker Hub

SSH into EC2 server

Pull latest images

Restart containers

This ensures fully automated deployment without manual intervention.

Nginx Reverse Proxy

Nginx is installed on the EC2 server and configured to listen on port 80.

Configuration example:

server {
listen 80;

location / {
    proxy_pass http://localhost:80;
}

location /api {
    proxy_pass http://localhost:5000;
}

}

The application is accessible using:

http://EC2_PUBLIC_IP

Local Development Setup

Backend:

cd backend
npm install
node server.js

Frontend:

cd frontend
npm install
ng serve --port 8081

Access locally:

http://localhost:8081

Screenshots

Include screenshots of:

GitHub Actions successful pipeline

Docker Hub repositories

EC2 instance dashboard

docker ps output

Application running in browser

Nginx configuration

Security group inbound rules

Security Practices

Docker credentials stored as GitHub Secrets

No hardcoded passwords

SSH key-based authentication

MongoDB isolated within Docker network

Navigate to `http://localhost:8081/`
