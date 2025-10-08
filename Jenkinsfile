pipeline {
    agent any
    environment {
        DOCKER_HUB_USER = 'vanshita0920'
        IMAGE_NAME = 'java-hello'
    }

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/vanshita0209/java-hello.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Use Windows batch command
                    bat "docker build -t ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest ."
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    // Windows batch login
                    bat "echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin"
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    // Push Docker image using Windows batch
                    bat "docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest"
                }
            }
        }
    }
}
