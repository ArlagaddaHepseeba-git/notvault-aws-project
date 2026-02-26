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


