    pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'habimanadaniel/jenkins_web_ap'
        DOCKER_CREDENTIALS_ID = 'e639f820-25b3-4b0d-85a5-196bad593e1b' // Jenkins credentials ID for Docker Hub
    }
    stages {

        stage('Build') {
            steps {
                echo "Building the project..."
                bat 'dir'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                // Add any Windows-friendly test commands here
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                bat """
                docker build -t %DOCKER_IMAGE%:latest .
                """
            }
        }

        stage('Push Docker Image') {
            steps {
                echo "Logging in and pushing Docker image to Docker Hub..."
                withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS_ID, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat """
                    docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                    docker push %DOCKER_IMAGE%:latest
                    """
                }
            }
        }

        stage('Deploy Docker Container') {
            steps {
                echo "Deploying Docker container locally..."
                bat """
                docker rm -f my-web-app || exit 0
                docker run -d --name my-web-app -p 8080:80 %DOCKER_IMAGE%:latest
                """
            }
        }

    }
}
