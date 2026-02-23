# 🚀 End-to-End CI/CD Pipeline using Jenkins, Maven, SonarQube, Nexus, Tomcat & Slack

## 📌 Project Description
### An automated end-to-end CI/CD pipeline built on AWS EC2 using Jenkins, integrating Git, SonarQube, Maven, Nexus, Tomcat and Slack to automate code integration, quality analysis, build, artifact management, deployment and team notifications.

## 🛠️ Tools & Technologies

### 1.AWS EC2 
### 2.Git 
### 3.GitHub 
### 4.Jenkins 
### 5.Maven
### 6.SonarQube 
### 7.Nexus 
### 8.Tomcat 
### 9.Slack 

## 🏗️ Architecture

<img width="2840" height="1572" alt="image" src="https://github.com/user-attachments/assets/eeee7367-72c0-480f-b71c-10ed29e78f8b" />

## 📋 Pipeline Stages

<img width="2386" height="306" alt="image" src="https://github.com/user-attachments/assets/f3d3ff8f-4fae-4a89-945e-c4ac69b92c5b" />

Let’s break down the pipeline into stages, each serving a unique purpose in the CI/CD process:

🧑‍💻 **Stage 1: Code (Git)**
Fetches the latest source code from the GitHub repository to start the pipeline.

🔍 **Stage 2: CQA - Code Quality Analysis (SonarQube)**
Scans the code for bugs, code smells and security vulnerabilities before the build.

🏗️ **Stage 3: Build & Unit Test (Maven)**
Compiles the source code and runs unit tests to make sure everything works fine.

📦 **Stage 4: Artifact (Nexus)**
Packages the application as a WAR file and uploads it to Nexus repository for storage.

🚀 **Stage 5: Deploy (Tomcat)**
Deploys the WAR file to the Tomcat server to make the application live.

📢 **Stage 6: Post Build Actions (Slack Notification)**
Sends a success or failure notification to the Slack channel after the pipeline completes.

## 🏗️ Practical Implementation of Project

Here I need 4 servers to implement this project.

1. **Jenkins**
   - AMI = Amazon Linux 2023
   - Instance type = t2.medium
   - EBS = 8 GB
   - Security Groups = SSH, 8080

2. **Tomcat**
   - AMI = Amazon Linux 2023
   - Instance type = t2.micro
   - EBS = 8 GB
   - Security Groups = SSH, 8080

3. **SonarQube**
   - AMI = Amazon Linux 2023
   - Instance type = t2.medium
   - EBS = 28 GB
   - Security Groups = SSH, 9000

4. **Nexus**
   - AMI = Amazon Linux 2023
   - Instance type = t2.medium
   - EBS = 28 GB
   - Security Groups = SSH, 8081

Let's launch all 4 servers on AWS EC2.

<img width="1920" height="1080" alt="EC2-INSTANCE" src="https://github.com/user-attachments/assets/f64c4ba0-2968-4be1-898f-042457406054" />

setup all the tools on their respective servers

1. **jenkins.sh**

 #STEP-1: INSTALLING GIT 
 yum install git  -y

 #STEP-2: GETTING THE REPO (jenkins.io --> download -- > redhat)
 sudo wget -O /etc/yum.repos.d/jenkins.repo \
     https://pkg.jenkins.io/redhat-stable/jenkins.repo
 sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

 #STEP-3: DOWNLOAD JAVA11 AND JENKINS
 yum install java-17-amazon-corretto -y
 yum install jenkins -y

 #STEP-4: RESTARTING JENKINS (when we download service it will on stopped state)
 systemctl start jenkins.service
 systemctl enable jenkins.service
 systemctl status jenkins.service




