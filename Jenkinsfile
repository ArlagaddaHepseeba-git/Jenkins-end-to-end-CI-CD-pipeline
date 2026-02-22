pipeline {
    agent any

    tools {
        maven 'maven3'
    }

    stages {

        stage('1 - Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ArlagaddaHepseeba-git/jenkins-end-to-end-ci-cd-pipeline.git'
            }
        }

        stage('2 - Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('3 - SonarQube Scan') {
            steps {
                withSonarQubeEnv('sonar-server') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('4 - Upload to Nexus') {
            steps {
                sh 'mvn deploy'
            }
        }

        stage('5 - Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat8(
                        credentialsId: 'tomcat-cred',
                        path: '',
                        url: 'http://YOUR_TOMCAT_IP:8080'
                    )
                ],
                contextPath: 'myweb',
                war: 'target/*.war'
            }
        }

    }

    post {
        success {
            echo 'BUILD SUCCESS!'
            slackSend channel: '#devops-alerts',
                      color: 'good',
                      message: "SUCCESS: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}"
        }
        failure {
            echo 'BUILD FAILED!'
            slackSend channel: '#devops-alerts',
                      color: 'danger',
                      message: "FAILED: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}"
        }
    }
}
