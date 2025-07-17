# 🐳 Two-Tier Flask + MySQL App with Docker Networking

This project demonstrates how to set up a **two-tier application** using **Docker containers**:  
- A **Flask-based frontend** running a simple web app  
- A **MySQL database backend**  
Connected via a **user-defined Docker bridge network** to enable inter-container communication.

---

## 🚀 What This Project Covers

- Launching an EC2 instance and SSH connection using a `.pem` file  
- Installing Docker on Ubuntu (WSL or EC2)  
- Cloning this repository  
- Building a custom Docker image for the Flask app  
- Creating a user-defined Docker network  
- Running MySQL and Flask app containers on the same network  
- Testing the application via browser and MySQL shell

---

## 🔧 Prerequisites

- AWS EC2 instance (Ubuntu preferred)
- Docker installed
- Git installed
- SSH access with PEM file

---

## 🐳 Docker Commands Used

### Build Flask App Image

```bash
docker build -t two-tier-app .
```

## Create Custom Network
```bash
docker network create two-tier -d bridge
```

## Run MySQL Container
```bash
docker run -d --name mysql --network two-tier \
  -e MYSQL_ROOT_PASSWORD=root \
  -e MYSQL_DATABASE=devops \
  mysql
```

## Run Flask App Container
```bash
docker run -d -p 5000:5000 --network two-tier \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=root \
  -e MYSQL_DB=devops \
  two-tier-app:latest

```

## 🌐 Access the App
Once both containers are running, open your browser and go to:
```bash
http://<your-ec2-public-ip>:5000
```
> Make sure port 5000 is open in your EC2 security group.

## 🧪 Check MySQL Database
```bash
docker exec -it <mysql_container_id> bash
mysql -u root -p

SHOW DATABASES;
USE devops;
SELECT * FROM messages;
```

Watch Tutorial on [YouTube](https://youtu.be/QkLbXp-bTj0?si=v6lXG-PFTeInLyMu)

## Connect with Me <br>
[dev.to](https://dev.to/prashant_gohel_321) | [YouTube](https://www.youtube.com/@DevOpsWithUs) | [LinkedIn](https://www.linkedin.com/in/prashantgohel1706)
