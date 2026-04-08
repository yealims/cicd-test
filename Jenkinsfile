pipeline {
    agent any

    environment {
        strDockerImage="yealims/cicd-test:0.1"
    }
    stages {
        stage('Github Pull') {
            steps {
                git branch: 'main', url: 'https://github.com/yealims/cicd-test.git'
            }
        }
        stage('Docker image build') {
            steps {
                script {
                    oDockImage = docker.build(strDockerImage, "-f Dockerfile .")
                }
            }
        }
        stage('Deploy Server') {
            steps {
                sshagent(credentials: ['Deploy-Privatekey']) {
                    sh "scp -o StrictHostKeyChecking=no index.html ubuntu@52.79.253.220:/home/ubuntu"
                    sh "ssh -o StrictHostKeyChecking=no ubuntu@52.79.253.220 sudo cp /home/ubuntu/index.html /var/www/html"
                }
            }
        }
    }
}