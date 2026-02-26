#  NoteVault

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?style=for-the-badge&logo=amazon-aws)
![Node.js](https://img.shields.io/badge/Node.js-Backend-green?style=for-the-badge&logo=node.js)
![MySQL](https://img.shields.io/badge/MySQL-Database-blue?style=for-the-badge&logo=mysql)
![Nginx](https://img.shields.io/badge/Nginx-Proxy-brightgreen?style=for-the-badge&logo=nginx)
![Status](https://img.shields.io/badge/Status-Live-success?style=for-the-badge)

#### > A secure, cloud-native Notes Management Application built and deployed on AWS from scratch — using 5 core AWS services with production-level architecture.

## 🌟 Project Overview

**NoteVault** is a full-stack REST API application where users can:
- ✅ Create notes
- ✅ View all notes
- ✅ Delete notes
- ✅ All data stored in a real cloud database (RDS MySQL)
- ✅ Deployed on a live AWS EC2 server

 ## 🏗️ Architecture Diagram

 <img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/3af8b07d-3051-4402-b3a0-2e462e000c04" />

 ## ☁️ AWS Services Used

| Service | Purpose | Configuration |
|---|---|---|
| **EC2** | Application Server | Amazon Linux 2023, t2.micro, Free Tier |
| **RDS** | MySQL Database | db.t3.micro, Private Subnet, Free Tier |
| **S3** | File Storage | notvault-files-2026, Mumbai Region |
| **VPC** | Network Isolation | Custom VPC, Public + Private Subnets |
| **IAM** | Security & Access | Custom User, Roles, Policies |



## 🔧 Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | Node.js, Express.js |
| **Database** | MySQL 8.0 (AWS RDS) |
| **Web Server** | Nginx (Reverse Proxy) |
| **Process Manager** | PM2 |
| **Cloud** | AWS (EC2, RDS, S3, VPC, IAM) |
| **OS** | Amazon Linux 2023 |


## 🚀 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Get all notes |
| POST | `/notes` | Create a new note |
| DELETE | `/notes/:id` | Delete a note by ID |
| GET | `/health` | Server health check |

### Sample API Responses:

**GET /** — List all notes:
```json
{
  "success": true,
  "notes": [
    {
      "id": 1,
      "title": "My First Note",
      "content": "NoteVault is working on AWS!",
      "created_at": "2026-02-26T04:11:39.000Z"
    }
  ]
}
```
**GET /health** — Health check:
```json
{
  "status": "NoteVault is Running!",
  "time": "2026-02-26T04:26:57.374Z"
}
```

**POST /notes** — Create note:
```json
// Request Body:
{
  "title": "AWS Note",
  "content": "Built on EC2, RDS, S3, VPC, IAM!"
}

// Response:
{
  "success": true,
  "noteId": 2
}














### 4. RDS Setup
```bash
# Created DB Subnet Group
# Launched MySQL 8.0 in private subnet
# Database: notvault_db
# Connected from EC2:
mysql -h [RDS-ENDPOINT] -u admin -p
```

### 5. EC2 Setup
```bash
# Launched Amazon Linux 2023 t2.micro
# SSH into server:
ssh -i notvault-key.pem ec2-user@[EC2-IP]

# Install dependencies:
sudo dnf update -y
sudo dnf install nodejs npm git nginx -y
sudo dnf install mysql8.0 -y

# Start Nginx:
sudo systemctl enable nginx
sudo systemctl start nginx
```

### 6. App Deployment
```bash
# Create project:
mkdir ~/notvault && cd ~/notvault
npm init -y
npm install express mysql2 dotenv

# Start with PM2:
sudo npm install -g pm2
pm2 start server.js --name notvault-app
pm2 startup
pm2 save
```

### 7. Nginx Configuration
```nginx
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_cache_bypass $http_upgrade;
    }
}
```

---

## 📸 Project Screenshots

### 1. NoteVault API — Live Response
> App returning real data from RDS MySQL database

![NoteVault Live](screenshots/notvault-live.png)



