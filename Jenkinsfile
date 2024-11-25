pipeline {
    agent any // Use any available Jenkins agent with Docker installed

    environment {
        DOCKER_IMAGE = "pg-finder:latest" // Define the Docker image name
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the code from the Git repository
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Enable BuildKit and build the Docker image
                    sh 'docker build -t ${DOCKER_IMAGE} .'
                }
            }
        }

        stage('Run Application') {
            steps {
                script {
                    // Run the Docker container
                    sh 'docker run -d -p 3000:3000 ${DOCKER_IMAGE}'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
        success {
            echo 'Application deployed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for details.'
        }
    }
}
