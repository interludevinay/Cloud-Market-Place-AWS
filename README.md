# 🛒 Cloud Market Place Clone - AWS Deployment

This repository contains a clone of a cloud-based marketplace application. The project is designed to be deployed on a Virtual Private Cloud (VPC) in AWS using public subnets across multiple Availability Zones for high availability and scalability.

---

## 🧱 Project Structure

- `src/` – Source code of the frontend application  
- `public/` – Static files  
- `dist/` – Production-ready build (created using `npm run build`)  
- `package.json` – Project metadata and dependencies  

---

## 🚀 Live Deployment Architecture (AWS)

![Image](https://github.com/user-attachments/assets/6ec6db01-e605-4085-bd4e-19e6f26e2bbd)

### 🔧 Architecture Components

- **VPC**: Isolated network environment  
- **Public Subnets (x2)**: One in each availability zone (AZ)  
- **Internet Gateway (IGW)**: Enables internet access  
- **EC2 Instances (x2)**: Hosting the frontend app via Nginx or Node.js  
- **Route Table**: Routes traffic from subnets to the internet  

---

## 📦 Technologies Used

- Node.js  
- Express (optional)  
- AWS EC2  
- AWS VPC  
- Nginx (or simple HTTP server)  
- Git  

---

## 🛠️ Local Development

### 1. Clone the repository

```bash
git clone https://github.com/interludevinay/Cloud-Market-Place.git
cd Cloud-Market-Place
```

### 2. Install dependencies
```bash
npm install
```

### 3. Build the project

```bash
npm run build
```
✅ This will generate the dist/ folder containing the production-ready build of the app.

# ☁️ AWS Deployment Guide (Manual)

This guide walks you through deploying the Cloud Market Place Clone on AWS using a manual setup with EC2 and a VPC in public subnets.

---

## 🧰 Prerequisites

Before you begin, make sure you have:

- ✅ An **AWS Account**
- ✅ **AWS CLI** configured (optional but helpful)
- ✅ An existing **SSH key pair** (`.pem` file)
- ✅ An **EC2 instance** in a **public subnet** with internet access

---

## 👣 Step-by-Step Deployment

### 🔹 Step 1: Provision Infrastructure (via AWS Console)

1. **Create a VPC**
   - CIDR Block: `10.0.0.0/16`

2. **Create Two Public Subnets**
   - Subnet 1: `10.0.1.0/24` in Availability Zone 1
   - Subnet 2: `10.0.2.0/24` in Availability Zone 2

3. **Create and Attach Internet Gateway (IGW)**
   - Attach the IGW to your VPC

4. **Create Route Table**
   - Add route `0.0.0.0/0` pointing to the IGW
   - Associate the route table with both public subnets

5. **Launch EC2 Instances**
   - Choose **Ubuntu** or **Amazon Linux**
   - Place the instance in a **public subnet**
   - **Enable auto-assign public IP**
   - Configure **Inbound Rules**:
     - Port 22 (SSH)
     - Port 80 (HTTP)

---

### 🔹 Step 2: Deploy the App on EC2

#### A. SSH into your EC2 instance

```bash
ssh -i "your-key.pem" ubuntu@<EC2-PUBLIC-IP>
```

### 🚀 Application Deployment on EC2

#### 🅰️ SSH into Your EC2 Instance

```bash
ssh -i "your-key.pem" ubuntu@<EC2-PUBLIC-IP>
```
> Replace `your-key.pem` with the name of your private key and `<EC2-PUBLIC-IP>` with the public IP of your EC2 instance.

---

#### 🅱️ Install Required Packages

```bash
sudo apt update
sudo apt install nginx git curl -y
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt install -y nodejs
```
OR
```
sudo apt update
sudo apt install nginx -y
```
---

#### 🆑 Clone the Repository on the EC2 Instance

```bash
git clone https://github.com/interludevinay/Cloud-Market-Place.git
cd Cloud-Market-Place
```
OR

Copy it to the EC2 instance from our local machine
```
scp -i ".pem" -r /path/file ubuntu@<EC2-PUBLIC-IP>:~/react-app

```

---

#### 🛠️ Build the Project

```bash
npm install
npm run build
```
> This will generate a `dist` folder containing the production-ready build of the application.

---

#### 📦 Serve the Build Using Nginx

```bash
sudo rm -rf /var/www/html/*
sudo cp -r dist/* /var/www/html/
```
> This will copy your frontend files into the Nginx default web directory.

---

#### 🔄 Restart Nginx

```bash
sudo systemctl restart nginx
```

---

#### 🌐 Access the App

Open your browser and go to:

```
http://<EC2-PUBLIC-IP>
```
> You should now see the Cloud Market Place frontend running successfully!
