pipeline {
    agent any

    stages {
        stage('Github Pull') {
            steps {
                git branch: 'main', url: 'https://github.com/yealims/cicd-test.git'
            }
        }
        stage('Git Clone End') {
            steps {
                sh 'touch cicd_test.txt'
                sh 'echo "git clone end" > cicd_test.txt'
            }
        }
        stage('Deploy Server') {
            steps {
                sshagent(credentials: ['Deploy-Privatekey']) {
                    sh "sudo scp -o StrictHostKeyChecking=no index.html ubuntu@52.79.253.220:/var/www/html/"
                }
            }
        }
    }
}