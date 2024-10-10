pipeline {
    agent any
    tools {nodejs "npm"}


    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        IMAGE_NAME = 'anujgarg01/eks-argo'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/AnujdotGarg/EKS-ARGO-NODE.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("$IMAGE_NAME:latest")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "$DOCKERHUB_CREDENTIALS") {
                    docker.image("$DOCKER_IMAGE:latest").push()
                    }
                }
            }
        }
    }
}

    

