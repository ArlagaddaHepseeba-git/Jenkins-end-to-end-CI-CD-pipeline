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
