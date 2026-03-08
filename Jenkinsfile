pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        DOCKERHUB_CREDENTIALS = "dockerhub-credentials-id"
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
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKERHUB_CREDENTIALS}") {
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh "docker run -d --rm -p 8080:8080 ${IMAGE_NAME}:latest"
                }
            }
        }
    }
}
