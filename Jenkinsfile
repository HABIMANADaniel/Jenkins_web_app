pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'habimanadaniel/jenkins_web_ap'
        DOCKER_CREDENTIALS_ID = 'Dani@1234'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        dockerImage.push('latest')
                    }
                }
            }
        }

        stage('Deploy to Local Docker Host') {
            steps {
                bat '''
                    docker rm -f my-web-app || true
                    docker run -d --name my-web-app -p 8080:80 yourdockerhubusername/my-web-app:latest
                '''
            }
        }

    }
}
