# Day 3 – AWS IAM, EC2, CI/CD Pipeline & Docker Setup

📅 **Date:** 29/03/2025

---

## 🧑‍💼 AWS IAM (Identity and Access Management)

We learned how to manage user access in AWS using IAM.

### 🔐 Steps to Create an IAM User

1. Go to **IAM** service on AWS Console.
2. Navigate to **Access Management > Users**.
3. Click on **Create User**.
4. Provide a **User Name**.
5. Check the box: **Provide user access to AWS Management Console**.
6. Choose: **User must create a new password**.
7. Select: **Attach policies directly**.
8. Check **AdministratorAccess**.
9. Click **Next** and then **Create User**.
10. Note down the **Console Sign-in link**, **User name**, and **Password**.

Now the user can log in with their credentials as an IAM user.

---

## 🖥️ AWS EC2 – Launching a Linux Instance

### 🔧 Steps to Launch an Instance

1. Go to **EC2** in AWS Console.
2. Click on **Launch Instance**.
3. Choose **Amazon Linux AMI**.
4. Select **Instance Type** (e.g., t2.micro – Free Tier).
5. Configure instance, add storage (default is fine), and configure security group.
6. Allow **SSH (port 22)** and optionally **HTTP (port 80)** access.
7. Create and download the **.ppk key pair**.
8. Launch the instance.

---

## 🔑 Download & Configure PuTTY for EC2 SSH Access

> Note: PuTTY uses `.ppk` format, convert `.pem` using PuTTYgen.

### 🛠 Steps:

1. Download and install **PuTTY** from Google.
2. Open **PuTTY**.
3. Under **Host Name**, enter: `ec2-user@<Public-IP>` from AWS EC2 console.
4. Go to **SSH > Auth** in the left menu.
5. Browse and select the `.ppk` file.
6. Click **Open**.

Once connected, you’ll see a Linux terminal. First thing to run:

```bash
sudo
sudo yum update -y
```
### 🐳 Docker Installation on EC2 (Amazon Linux)

Make sure PuTTY session is active before running:
```bash
sudo yum update -y
sudo yum install -y docker
sudo systemctl start docker
sudo systemctl enable docker
docker --version
```
✅ If docker --version gives an output, Docker is installed.

### 🚀 CI/CD Pipeline – Concept Overview

A basic CI/CD pipeline was demonstrated as follows:
```
START ➝ IAM User ➝ EC2 Linux Instance ➝ Dev Policy ➝ CI Config ➝ Docker ➝ Deploy Application ➝ END
```
Mini Pipelines were introduced (e.g., adding new features).

*Hands-on practice included deploying a small HTML/NodeJS app.*

### 🐳 Docker Commands Used
```bash
cd Calculator_using_htmlcssjs   
docker ps  
ls -la  
pwd  
nano Dockerfile  
```
### 🛠 Dockerfile Example
```bash
# Use the BusyBox image with httpd
FROM busybox:latest

# Set the working directory inside the container
WORKDIR /www

# Copy static website files
COPY . /www

# Expose port 80
EXPOSE 80

# Run HTTP server
CMD ["httpd", "-f", "-v", "-p", "80"]
```
### 🔧 Build & Run Docker Container
```bash
docker build -t my-app .
docker run -d -p 80:80 my-app
```
In EC2 Security Group:

    Go to Security Groups > launch-wizard

    Click Edit Inbound Rules

    Add All traffic or Custom TCP 80

    Set Source as Anywhere (IPv4)

    Save rules

### 🌐 Access the App

Open browser and enter:
```bash
http://<Public-IP>
```
*You should see the deployed web app.*