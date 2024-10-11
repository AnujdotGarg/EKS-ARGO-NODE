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
                git branch: 'main', url: 'https://github.com/AnujdotGarg/EKS-ARGO-NODE.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("$IMAGE_NAME:$BUILD_NUMBER")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                    docker.image("$IMAGE_NAME:$BUILD_NUMBER").push()
                    }
                }
            }
        }
    }
}

    

