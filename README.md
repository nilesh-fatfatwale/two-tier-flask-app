# 🚀 Flask App with MySQL – Docker Setup + Jenkins CICD

This is a simple Flask application that interacts with a MySQL database. Users can submit messages via a frontend form, which are then stored in a MySQL database and displayed on the frontend.

---

## 📋 Prerequisites

Make sure the following are installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Git](https://git-scm.com/) 

---

## 📦 Setup

### 1. Clone the Repository

```bash
git clone https://github.com/nilesh-fatfatwale/two-tier-flask-app
cd two-tier-flask-app
```
🔹 Run with Dockerfile (Manual Setup):

1. Build the Flask App Image
```bash
docker build -t flaskapp .
```

🌐 2. Create Docker Network
```bash
docker network create twotier
```
🐬 3. Run MySQL Container
```bash
docker run -d \
  --name mysql \
  -v mysql-data:/var/lib/mysql \
  --network=twotier \
  -e MYSQL_DATABASE=mydb \
  -e MYSQL_ROOT_PASSWORD=admin \
  -p 3306:3306 \
  mysql:5.7
```
🚀 4. Run Flask App Container
```bash
docker run -d \
  --name flaskapp \
  --network=twotier \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=admin \
  -e MYSQL_DB=mydb \
  -p 5000:5000 \
  flaskapp:latest
```
🔹 Method 2: Run with Docker Compose (Easy Setup)
▶️ 1. Start with Docker Compose
```bash
docker-compose up --build
```
🧹 Stop the Setup
```bash
docker-compose down
```
🌐 Access the App
http://localhost:5000

