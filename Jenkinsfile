pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/SaiAbhijith21/nginx-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nginx-app:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop nginx-container || true'
                sh 'docker rm nginx-container || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name nginx-container -p 80:80 nginx-app:latest'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps | grep nginx-container'
            }
        }
    }

    post {
        success {
            echo 'Nginx deployed successfully!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}