pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'joannedada/webappcal'   // Replace with your Docker Hub username
        DOCKER_CREDENTIALS_ID = 'dockerhub-credentials'  // Jenkins credentials ID for Docker Hub
    }

    stages {
        stage('Clone Repo') {
            steps {
                // Clone the Git repository
                git branch: 'dev', url:'https://github.com/joannedada/JavaWeb3.git'   // Use your GitHub repository
            }
        }

        stage('Build WAR') {
            steps {
                // Build the WAR file using Maven
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image from the Dockerfile
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the built Docker image to Docker Hub
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        docker.image("${DOCKER_IMAGE}").push('latest')
                    }
                }
            }
        }
    }
}
