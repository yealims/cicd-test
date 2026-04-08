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
        stage('Docker Image Push') {
            steps {
                script {
                    docker.withRegistry('','docker-auth'){
                        oDockImage.push()
                    }
                }
            }
        }
        stage('Deploy Server') {
            steps {
                sshagent(credentials: ['Deploy-Privatekey']) {
                    sh "ssh -o StrictHostKeyChecking=no ubuntu@52.79.253.220 docker container rm -f sampleweb "
                    sh "ssh -o StrictHostKeyChecking=no ubuntu@52.79.253.220 docker run -d -p 80:80 --name sampleweb ${strDockerImage}"
                }
            }
        }
    }
}