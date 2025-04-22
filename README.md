User Service
This project is the User Service that is used behind the API Gateway.

It is a Spring Boot application deployed on Google Kubernetes Engine (GKE).

📚 Table of Contents
🚀 Deployment Overview

🛠 Setup Instructions

1. Build Docker Image

2. Push Docker Image to Docker Hub

3. Update Kubernetes Deployment File

4. Deploy to GKE

📂 Folder Structure

📣 Related Projects

🙏 Contribution

✨ Maintained by

🚀 Deployment Overview
We are using the Kubernetes deployment file:

deployment-dns-master-01.yaml

This file contains the working deployment setup for GKE.

The service URL, database credentials, and application configuration are passed via environment variables.

🛠 Setup Instructions
Follow these steps carefully:

1. Build Docker Image
Build your Docker image for the user service:

docker build -t <your-dockerhub-username>/user-service:<version> .

Example:

docker build -t shaikh79/user-service1:2.0.1 .

2. Push Docker Image to Docker Hub

docker push <your-dockerhub-username>/user-service:<version>
Example:

docker push shaikh79/user-service1:2.0.1
3. Update Kubernetes Deployment File
Open deployment-dns-master-01.yaml and update the following fields:


Field	Update

image	Update to your correct Docker image
SPRING_DATASOURCE_URL	Update with your Database URL
SPRING_DATASOURCE_USERNAME	Update with your DB username
SPRING_DATASOURCE_PASSWORD	🚨 Do not hardcode passwords! Use Kubernetes Secrets or placeholder values
SPRING_JPA_HIBERNATE_DDL_AUTO	Set based on your needs (usually update)
❗ Important:

Never push real database credentials to GitHub.

Always use Kubernetes Secrets for sensitive information.

Example snippet:

yaml
Copy
Edit
- name: SPRING_DATASOURCE_URL
  value: "db-url"
- name: SPRING_DATASOURCE_USERNAME
  value: "your-database-username"
- name: SPRING_DATASOURCE_PASSWORD
  value: "your-db-password" # <-- REMOVE this!
4. Deploy to GKE
Make sure you are connected to your GKE cluster, then apply the deployment:


kubectl apply -f deployment-dns-master-01.yaml
Check if pods and service are running:


kubectl get pods
kubectl get svc

📂 Folder Structure

user-service/
├── src/
├── deployment-dns-master-01.yaml
├── Dockerfile
├── README.md
└── pom.xml
📣 Related Projects
API Gateway Project

🙏 Contribution
If you find any issues or have suggestions, feel free to open a Pull Request.

✨ Maintained by
FC-JAVA-TEAM

