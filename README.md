# STATIC WEB PAGE DEPLOYMENT USING JENKINS AND TERRAFORM 

## 📋 Project Description
This project demonstrates how to deploy a static website on an EC2 instance using infrastructure-as-code with Terraform, and automate updates through a Jenkins CI/CD pipeline with GitHub webhooks.

## 🎯 Project Requirements

### Repository Setup
- Forked from: `https://github.com/Dhanrajdk79/Static_web_page_deployment_using_jenkins_terraform.git`
- Make visible UI changes and commit them to trigger automation

### Terraform Requirements
- Create an EC2 instance with proper configuration
- Create Security Group allowing HTTP traffic (port 80)
- Use User Data script to:
  - Install Nginx/Apache web server
  - Clone the repository into `/var/www/html`
  - Set proper file permissions

### Jenkins Pipeline Requirements
- Trigger pipeline automatically using GitHub webhooks
- Pull the latest code from repository
- SSH into EC2 instance
- Pull updates into the web root directory
- Restart Nginx/Apache service
- Validate that website reflects the new changes

## 🏗️ Architecture Overview

```
GitHub Repository → Jenkins CI/CD Pipeline → EC2 Instance (Nginx) → End Users
       ↑                    ↓                      ↓
   Webhook Trigger     SSH Deployment      Static Website Serving
```

## 📁 Project Structure

```
static_web_page_deployment/
├── HomePage.html
├── Homepage.css
├── jenkinsfile
├── main.tf
├── Projectpage.html
├── Projectpage.css
├── Servicepage.html
├── Servicepage.css
├── blog.html
├── blog.css
└── README.md
```

## 🛠️ Implementation Details

### Terraform Infrastructure
- **EC2 Instance**: Ubuntu-based instance deployed in us-east-1 region
- **Security Group**: Configured to allow HTTP (port 80) and SSH (port 22) access
- **User Data Script**: Automated web server installation and repository setup

### Jenkins Pipeline Stages
1. **Checkout SCM** - Fetch source code from GitHub repository
2. **Prepare Remote** - Set up SSH connection to EC2 instance
3. **Upload & Deploy** - Transfer files and update web server
4. **Smoke Test** - Validate deployment success

### Credentials Management
- SSH keys configured in Jenkins for secure EC2 access
- Multiple credentials for different deployment scenarios

## 📸 Implementation Evidence

### Infrastructure Components
- **EC2 Instance**: `i-0e370e313b2fc57ae` (static-web-server)
- **Public IP**: `54.236.250.105`
- **Region**: us-east-1
- **Instance Type**: t2.micro

### Jenkins Pipeline Performance
- **Average Build Time**: ~9 seconds
- **Successful automated deployments** with GitHub webhook triggers
- **Pipeline Stages**:
  - Checkout SCM: 444ms
  - Prepare Remote: 49s
  - Upload & Deploy: 680ms
  - Smoke Test: 201ms

### Web Server Details
- **Web Root**: `/var/www/html`
- **Server**: Nginx/Apache
- **Access**: Publicly accessible via HTTP

## 🚀 Deployment Process

1. **Infrastructure Provisioning**:
   ```bash
   terraform init
   terraform plan
   terraform apply
   ```

2. **Jenkins Pipeline Setup**:
   - Configure GitHub webhooks
   - Set up SSH credentials for EC2 access
   - Create Jenkins pipeline job

3. **Automated Deployment**:
   - Commit changes to GitHub repository
   - Webhook triggers Jenkins pipeline
   - Pipeline automatically deploys updates to EC2
   - Website updates are live within seconds

## ✅ Validation

The deployment is validated through:
- Successful pipeline execution in Jenkins
- Website accessibility via public IP
- Visible UI changes reflecting latest commits
- Smoke tests confirming service availability

## 📈 Results

- **Successful static website deployment** on AWS EC2
- **Fully automated CI/CD pipeline** using Jenkins
![](images/code.PNG)
- **Infrastructure-as-Code** implementation with Terraform
![](images/jenkins.PNG)
- **Rapid deployment cycles** (~9 seconds average)
- **Zero-downtime updates** during deployments

This project demonstrates a complete DevOps workflow for static website deployment with full automation from code commit to production deployment.