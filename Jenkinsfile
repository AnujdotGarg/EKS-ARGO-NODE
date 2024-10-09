pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('049e6933-5ee8-4513-a9cd-c4d8308ffa3c')
        GIT_REPO_URL = 'git@github.com:AnujdotGarg/EKS-ARGO-NODE.git'

    }

    stages {
        stage('Checkout Code') {
            steps {
                git ( branch: 'main',
                url: "${env.GIT_REPO_URL}" )
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("docker push anujgarg01/eks-argo:$BUILD_NUMBER")
                }
            }
        }

        stage('Push Docker Image to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${env.DOCKERHUB_CREDENTIALS}") {
                        dockerImage.push('$BUILD_NUMBER')
                    }
                }
            }
        }

    }

    post {
        always {
            cleanWs()
        }
    }
}
