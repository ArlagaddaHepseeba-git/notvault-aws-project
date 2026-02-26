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
```


## 🗄️ Database Schema

```sql
CREATE DATABASE notvault_db;

USE notvault_db;

CREATE TABLE notes (
  id         INT AUTO_INCREMENT PRIMARY KEY,
  title      VARCHAR(255) NOT NULL,
  content    TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## 🔐 Security Architecture

| Security Feature | Implementation |
|---|---|
| **IAM User** | Separate admin user (no root access) |
| **IAM Role** | EC2-S3-BlogRole (no hardcoded credentials) |
| **Private Subnet** | RDS has zero internet exposure |
| **Security Groups** | EC2-SG (ports 22, 80, 3000) + RDS-SG (port 3306 from EC2 only) |
| **VPC Isolation** | Custom network — complete isolation |


## 🌐 Network Architecture

| Resource | CIDR / Value | Purpose |
|---|---|---|
| VPC | 10.0.0.0/16 | Main private network |
| Public Subnet | 10.0.1.0/24 | EC2 lives here |
| Private Subnet 1 | 10.0.2.0/24 | RDS lives here |
| Private Subnet 2 | 10.0.3.0/24 | RDS Multi-AZ |
| Internet Gateway | notvault-igw | Internet access for EC2 |
| Route Table | notvault-public-rt | Routes traffic to IGW |


## ⚙️ Setup & Deployment Steps

### 1. IAM Setup
```bash
# Created IAM user: notvault-admin
# Attached: AdministratorAccess policy
# Created IAM Role: EC2-S3-BlogRole
# Configured AWS CLI:
aws configure
```

### 2. VPC Setup
```bash
# Created VPC: notvault-vpc (10.0.0.0/16)
# Created Internet Gateway: notvault-igw
# Created 3 Subnets (public + 2 private)
# Created Route Table with IGW route
# Created Security Groups for EC2 and RDS
```

### 3. S3 Setup
```bash
# Created bucket: notvault-files-2026
aws s3 mb s3://notvault-files-2026
aws s3 cp test.txt s3://notvault-files-2026/uploads/
```

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

## 📸 Project Screenshots

### 1. NoteVault API — Live Response
> App returning real data from RDS MySQL database

<img width="1920" height="1080" alt="1 Browser " src="https://github.com/user-attachments/assets/04f9c704-af70-4705-ada0-c7717fca7102" />




### 2. Health Check — Server Running
> Server health check confirming EC2 is live

<img width="1920" height="1080" alt="2 Browser health" src="https://github.com/user-attachments/assets/3d8855a0-f1d5-4ee8-898f-03482df87e7c" />



### 3. EC2 Instance — Running
> EC2 server running on AWS Mumbai region

<img width="1920" height="1080" alt="3 EC2" src="https://github.com/user-attachments/assets/c3227b88-332a-42db-9872-0a12f2177986" />

<img width="1920" height="1080" alt="3 EC2 console running1" src="https://github.com/user-attachments/assets/6ba7fc22-ce08-4a78-a471-d90ef3e3172f" />

![Uploading 3.EC2 console running2.png…]()



### 4. RDS Database — Available
> MySQL database available in private subnet

<img width="1920" height="1080" alt="4 RDS Available" src="https://github.com/user-attachments/assets/bb744a65-f941-4a07-8ec2-54fe40a125a9" />



### 5. VPC — Custom Network
> Custom VPC with public and private subnets

<img width="1920" height="1080" alt="5 VPC Console" src="https://github.com/user-attachments/assets/47bcf284-0206-4fba-8e34-db5aecebcafb" />

<img width="1920" height="1080" alt="5 public  private subnets" src="https://github.com/user-attachments/assets/9860dce6-74f0-4de2-bd8b-15441d0c3d79" />



### 6. IAM User — Created
> IAM admin user with proper permissions

<img width="1920" height="1080" alt="IAM noteVault sucess" src="https://github.com/user-attachments/assets/7cd2e005-f5a8-47bb-be38-027a2ae5c1ca" />




### 7. S3 Bucket — Created
> S3 bucket for file storage

<img width="1920" height="1080" alt="s3 bucket running 2026" src="https://github.com/user-attachments/assets/50b1d051-ac63-4d3b-b0ed-b9dad85e67e3" />


## 💰 AWS Cost

| Service | Free Tier Limit | Cost |
|---|---|---|
| EC2 t2.micro | 750 hours/month | $0.00 |
| RDS db.t3.micro | 750 hours/month | $0.00 |
| S3 Storage | 5 GB | $0.00 |
| VPC | Free | $0.00 |
| IAM | Free | $0.00 |
| **Total** | | **$0.00** |


## 🎯 Key Learnings

- ✅ Designed **3-tier architecture** (Nginx → Node.js → MySQL)
- ✅ Secured database in **private subnet** — zero internet exposure
- ✅ Used **IAM Roles** instead of hardcoded AWS credentials
- ✅ Configured **Nginx** as reverse proxy with **PM2** process manager
- ✅ Implemented **VPC** with proper public/private subnet isolation
- ✅ Achieved **100% AWS Free Tier** deployment
- ✅ Connected **5 AWS services** in a single production-grade project

---
## 📌 What I Would Add Next

- [ ] CloudFront CDN for faster content delivery
- [ ] Route 53 for custom domain
- [ ] HTTPS with SSL Certificate (ACM)
- [ ] Auto Scaling Group for high availability
- [ ] CloudWatch monitoring and alerts
- [ ] Load Balancer for traffic distribution

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<div align="center">

**Built with ❤️ by Arlagadda Hepseeba**



</div>
















