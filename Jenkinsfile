pipeline {
    agent any
    tools {nodejs "npm"}


    environment {
        DOCKERHUB_CREDENTIALS = credentials('Dockerhub-creds')
        GIT_REPO_URL = 'https://github.com/AnujdotGarg/EKS-ARGO-NODE.git'
        IMAGE_NAME = 'anujgarg01/eks-argo'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git (branch: "main", 
                url: "${env.GIT_REPO_URL}" )
            }
        }

        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME:$BUILD_NUMBER ."
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD"
                sh "docker push $IMAGE_NAME:$BUILD_NUMBER"
            }
        }
    }
}

    

