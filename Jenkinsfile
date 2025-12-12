pipeline {
    agent any  // Runs on any available agent

    stages {
        stage('Build') {
            steps {
                echo "Building the project..."
                bat 'dir'   // Windows command
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                // Add your Windows test commands here
                // bat 'your-test-command'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying..."
                // Deployment commands for Windows
                // bat 'deploy-command'
            }
        }
    }
}
