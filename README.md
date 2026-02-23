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

1. **jenkins server**

<img width="1920" height="1080" alt="jenkins server" src="https://github.com/user-attachments/assets/026cd884-189d-47b5-83ed-d1b54fa9f196" />

2. **Tomcat server**

   <img width="1920" height="1080" alt="tomcat server" src="https://github.com/user-attachments/assets/4453ae5e-6b3e-43fb-9630-541d3c13e3c3" />

   <img width="1920" height="1080" alt="tomcat" src="https://github.com/user-attachments/assets/04c6681e-8a0d-4ffb-82bd-82fb61ee1a50" />

3. **Sonar server**
   
   <img width="1920" height="1080" alt="sonar server" src="https://github.com/user-attachments/assets/8a3109d0-1e4b-4506-b2b2-13ebbdb549b8" />

   <img width="1920" height="1080" alt="sonarqube" src="https://github.com/user-attachments/assets/67230dc6-3902-4cf9-8913-d2861fd86228" />


4. **nexus server**

   <img width="1920" height="1080" alt="nexus server" src="https://github.com/user-attachments/assets/cf1116f2-2cef-4fa3-bbee-631289d17008" />

   <img width="2880" height="1516" alt="image" src="https://github.com/user-attachments/assets/ec8517e5-f836-4091-bbf4-0fb77eb6a7d6" />

   <img width="1920" height="1080" alt="nexus new passwd" src="https://github.com/user-attachments/assets/55dba1a9-2139-4029-a291-0f4f1c46bf3c" />


   Create a repository in nexus

   SELECT REPOSITORIES

   <img width="1920" height="1080" alt="nexus repo" src="https://github.com/user-attachments/assets/5cae2f42-58f8-4456-88db-cda75ba66615" />

   SELECT CREATE-REPOSITORY

   <img width="1374" height="644" alt="image" src="https://github.com/user-attachments/assets/64844ae6-16a6-4e27-adb7-a565fcc8c13c" />

   SELECT MAVEN2(HOSTED)

   <img width="2866" height="1380" alt="image" src="https://github.com/user-attachments/assets/d29209d4-33d0-4f08-9dec-3df299721c4a" />

   I GIVE REPOSITORY NAME AS myrepo and deployment policy as Allow redeploy and click on create repositories

   <img width="2880" height="1112" alt="image" src="https://github.com/user-attachments/assets/eba84ec2-cd4e-4b14-95ec-8233b3a48330" />

   now repository created in dashboard

   <img width="1920" height="1080" alt="myrepo" src="https://github.com/user-attachments/assets/849eae71-561b-4212-98b5-390afff16cde" />

   After setting all the tools using above scripts, now we have to integrate with Jenkins. and install the required plugins to deploy an application.
   
   <img width="1920" height="1080" alt="plugins" src="https://github.com/user-attachments/assets/23df4422-9f74-4ce1-a75d-817990188ef3" />
   

   After installing all the plugins, now integrate sonarqube

   go to manage jenkins » system » and search for SonarQube servers

   Name: mysonar

   Server URL : sonarqube server url

   <img width="1920" height="1080" alt="sonar credential" src="https://github.com/user-attachments/assets/80be22e5-d1c4-4128-ad4c-58e4b192e75e" />

    It will ask the secret. To get the secret go to sonarqube dashboard and select your profile and click on My Account

    <img width="1920" height="1080" alt="sonar token" src="https://github.com/user-attachments/assets/56cfc424-cf7d-41e4-8b8c-4298200ae741" />

   Sonar credentials

   <img width="1920" height="1080" alt="Sonar credentials" src="https://github.com/user-attachments/assets/d8e5cffe-03b9-4546-a829-e305b47618d5" />

   Now go to manage jenkins » tools

   <img width="1920" height="1080" alt="sonar tool" src="https://github.com/user-attachments/assets/ac441ef2-03a4-4436-93dc-205496630b5f" />

   <img width="1920" height="1080" alt="maven" src="https://github.com/user-attachments/assets/c9b0d2b7-f317-400f-adcc-cde157d622b8" />

   After adding maven and sonar tools, just click on save

 ##  💬 Create a Free Slack Account

   Enter the company name

   <img width="1920" height="1080" alt="slackk project" src="https://github.com/user-attachments/assets/6c83988f-dfec-45b7-959d-b6b19efae0f6" />

   Click on Next

  Add teammate mail id’s

  Enter project name

  Select the free limited version

  <img width="1920" height="1030" alt="slack version" src="https://github.com/user-attachments/assets/d66fd40c-312c-4a89-91a8-11e8818bca26" />

  Now click on your company name (Mini-Project) » Tools & Settings » Manage apps

  <img width="1920" height="1080" alt="apps" src="https://github.com/user-attachments/assets/bd09676c-745d-4957-87aa-8e0756c3a4ea" />

  Now click on add to slack

  <img width="1920" height="1080" alt="jenkins ci" src="https://github.com/user-attachments/assets/d9ad6961-bc9e-4b96-bca8-effb03f9a106" />

  click on Add Jenkins CI Integration

  Now select the channel

  <img width="1920" height="1080" alt="new channel" src="https://github.com/user-attachments/assets/ab07e88d-1174-4fce-bc2c-78bcc72d8dd5" />

  click on Add Jenkins CI Integration

 From the step-3 copy the Team subdomain & Token

  <img width="1920" height="1080" alt="token" src="https://github.com/user-attachments/assets/53e5066f-39ed-4e52-8a15-cf4a8a92f0c0" />

  Go back to Jenkins and manage jenkins and search for slack

  Workspace : miniproject-1j17440

  Credentials ——> kind: Secret (add that token here)

  <img width="1920" height="1080" alt="slack sucess" src="https://github.com/user-attachments/assets/28f223f7-96d4-40f0-a975-f3e13e89e5ce" />

 ### Now add tomcat and nexus credentials
  
  go to manage jenkins » credentials » system » Global credentials (unrestricted)

  <img width="1920" height="1080" alt="tomcat credentials" src="https://github.com/user-attachments/assets/23c43034-a8bb-4cc0-a63e-4a61334e001a" />

  <img width="1920" height="1080" alt="nexus passwd" src="https://github.com/user-attachments/assets/6022bfd3-fb06-43f3-a267-94df94e1c4ff" />

  click on Create,and see the list of credentials like this

  <img width="1920" height="1080" alt="all credentials" src="https://github.com/user-attachments/assets/5e4424b7-7b3b-4a11-bfd4-4cdec901c27f" />

  After adding the credentials, write the pipeline like this


  pipeline {
    agent any
    tools {
        maven "mymaven"
    }
    stages {
        stage('Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ArlagaddaHepseeba-git/jenkins-end-to-end-ci-cd-pipeline.git'
            }
        }
        stage('CQA') {
            steps {
                withSonarQubeEnv('mysonar') {
                    sh '''
                        mvn sonar:sonar \
                        -Dsonar.projectKey=MyProject \
                        -Dsonar.host.url=http://54.85.1.178:9000 \
                        -Dsonar.login=4b4434c4157764adea0d1e968981ed7c8d9afc5c
                    '''
                }
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Artifact') {
            steps {
                nexusArtifactUploader(
                    artifacts: [[
                        artifactId: 'myweb',
                        classifier: '',
                        file: 'target/myweb-8.7.3.war',
                        type: 'war'
                    ]],
                    credentialsId: 'nexus',
                    groupId: 'in.javahome',
                    nexusUrl: '54.209.161.173:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'myrepo',
                    version: '8.7.3'
                )
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat',
                        path: '',
                        url: 'http://100.53.178.163:8080'
                    )
                ],
                contextPath: 'myapp',
                war: 'target/*.war'
            }
        }
    }
    post {
        always {
            echo 'Slack Notifications'
            slackSend(
                channel: '#new-channel',
                message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info: ${env.BUILD_URL}"
            )
        }
    }
}





## ✅ Pipeline Output

<img width="1920" height="1080" alt="my deployment build" src="https://github.com/user-attachments/assets/5a43309b-e3a9-451e-833d-9ac7fa2bdfe0" />

## 🔍 SonarQube Output

<img width="1920" height="1080" alt="sonarqube passed" src="https://github.com/user-attachments/assets/b91a289b-c6a8-4ed2-8a1f-692a36d0d2ff" />

## 📦 Nexus Output

<img width="1920" height="1080" alt="time nexus output" src="https://github.com/user-attachments/assets/2a06a340-a6a8-4cdd-a051-19dc3fa636a4" />


## 🌐Tomcat Output

<img width="1920" height="1080" alt="time techstore" src="https://github.com/user-attachments/assets/ac148bd4-b220-48aa-aba9-79503ede1ef1" />


## 🔔SLACK NOTIFICATION:

<img width="1920" height="1080" alt="time slack sucess" src="https://github.com/user-attachments/assets/dc4c624a-e326-4983-9140-7b96d2e126c0" />





  














   

  







   



   
   







