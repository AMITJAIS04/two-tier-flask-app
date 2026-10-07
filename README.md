# Two-Tier Web Application using Docker

## 📌 Project Overview

This project demonstrates the deployment of a two-tier web application using Docker on an AWS EC2 instance.

The application consists of two containers:

- **Flask Application** – Handles the web application.
- **MySQL Database** – Stores the application data.

Both containers communicate through a custom Docker network, and a Docker volume is used to persist MySQL database data.

---

## 🏗️ Architecture

```text
                         AWS EC2 Instance
                                |
                         Docker Compose
                                |
                    ┌───────────┴───────────┐
                    |                       |
              Flask App                 MySQL 8.4
               Container                Container
                    |                       |
                    └────── twotier ────────┘
                                            |
                                      mysql-data
                                         Volume
Architecture Components
AWS EC2 – Hosts the Docker containers.
Flask App Container – Runs the Flask web application on port 5000.
MySQL Container – Runs MySQL 8.4 and stores application data.
Docker Network (twotier) – Allows the Flask application to communicate with MySQL.
Docker Volume (mysql-data) – Provides persistent storage for MySQL data.
Docker Compose – Defines and manages the Flask and MySQL services.
🛠️ Technologies Used
AWS EC2
Docker
Docker Compose
Flask
MySQL 8.4
Linux
Docker Network
Docker Volume
Python
📁 Project Structure
two-tier-flask-app/
│
├── Dockerfile
├── Dockerfile-multistage
├── docker-compose.yml
├── app.py
├── message.sql
├── requirements.txt
├── requirements-dev.txt
├── Makefile
├── Jenkinsfile
├── templates/
├── k8s/
├── eks-manifests/
└── Screenshots/
🚀 Deployment
1. Clone the Repository
git clone <repository-url>
cd <repository-name>
2. Build and Start the Containers
docker compose up -d --build

This command builds the Flask application image and starts both the Flask and MySQL containers.

3. Check Running Containers
docker ps
4. Check Docker Network
docker network ls

The application and MySQL containers communicate through the twotier network.

5. Check Docker Volume
docker volume ls

The mysql-data volume is used to persist MySQL database data.

🔗 Application Access

The Flask application runs on port 5000.

After deploying the application on AWS EC2, it can be accessed using:

http://<EC2-Public-IP>:5000

The required port must be allowed in the EC2 Security Group.

💾 Database Persistence

MySQL data is stored using a Docker named volume:

mysql-data:/var/lib/mysql

This allows database data to persist even if the MySQL container is removed and recreated.

❤️ Health Checks

Docker Compose includes health checks for both services.

The Flask application waits for the MySQL service to become healthy before starting.

MySQL health is checked using mysqladmin ping.

📸 Project Screenshots
Application Running

Docker Containers & MySQL Data

AWS Security Group

AWS EC2 Instance

Docker Volume & Network

📚 Key Learnings

Through this project, I gained hands-on experience with:

Building Docker images using a Dockerfile
Running a Flask application inside a Docker container
Running MySQL in a separate container
Using Docker Compose to manage multiple containers
Creating and using a custom Docker network
Using Docker volumes for database persistence
Configuring AWS EC2 Security Groups
Deploying and accessing a containerized application on AWS EC2

### One important point

I would **not add Jenkins, Kubernetes, EKS, or the multistage Dockerfile to the deployment explanation yet**, even though those files exist in your repository. Those may be additional files/features from the original project, and we shouldn't claim you used them in *this deployment* unless we verify them.

For the README you're currently documenting, the important actual flow from your Compose file is:

**AWS EC2 → Docker Compose → Flask Container + MySQL Container → Docker Network + Docker Volume.**

Also, your screenshot filenames contain spaces, so the `%20` in the README image paths is intentional and important for GitHub.
