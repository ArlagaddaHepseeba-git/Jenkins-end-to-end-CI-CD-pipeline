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

<img width="1920" height="1080" alt="jenkins server" src="https://github.com/user-attachments/assets/026cd884-189d-47b5-83ed-d1b54fa9f196" />

2. **Tomcat.sh**

   <img width="1920" height="1080" alt="tomcat server" src="https://github.com/user-attachments/assets/4453ae5e-6b3e-43fb-9630-541d3c13e3c3" />

   <img width="1920" height="1080" alt="tomcat" src="https://github.com/user-attachments/assets/04c6681e-8a0d-4ffb-82bd-82fb61ee1a50" />

3. **Sonar.sh**
   
   <img width="1920" height="1080" alt="sonar server" src="https://github.com/user-attachments/assets/8a3109d0-1e4b-4506-b2b2-13ebbdb549b8" />

   <img width="1920" height="1080" alt="sonarqube" src="https://github.com/user-attachments/assets/67230dc6-3902-4cf9-8913-d2861fd86228" />

4. **nexus.sh**

   <img width="1920" height="1080" alt="nexus server" src="https://github.com/user-attachments/assets/cf1116f2-2cef-4fa3-bbee-631289d17008" />

   <img width="2880" height="1516" alt="image" src="https://github.com/user-attachments/assets/ec8517e5-f836-4091-bbf4-0fb77eb6a7d6" />

   Create a repository in nexus

   SELECT REPOSITORIES


   <img width="1920" height="1080" alt="nexus repo" src="https://github.com/user-attachments/assets/5cae2f42-58f8-4456-88db-cda75ba66615" />


   



   
   







