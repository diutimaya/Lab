pipeline {
    agent any

    environment {
        // Name of the docker image
        IMAGE_NAME = 'assn27-app'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the version control system
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building the Docker image for the Unified App (React + Express)...'
                // Use 'bat' instead of 'sh' since Jenkins agent is running natively on Windows
                bat "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Deploy / Run') {
            steps {
                echo 'Starting the application and dependencies (MongoDB) using Docker Compose...'
                bat 'docker compose down'
                bat 'docker compose up -d'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution finished.'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the Jenkins logs for more details.'
        }
    }
}
