pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials') // Replace with your Docker Hub credentials ID
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }

        stage('Build') {
            steps {
                sh "npm run build"
            }
        }

        stage('Dockerize') {
            steps {
                script {
                    def dockerImage = docker.build("your-dockerhub-username/your-image-name:${env.BUILD_NUMBER}")
                    dockerImage.push()
                }
            }
        }

        stage('Deploy to Docker Hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'DOCKER_HUB_CREDENTIALS', variable: 'DOCKER_HUB_CREDENTIALS')]) {
                        sh """
                        docker login -u your-dockerhub-username -p "\$DOCKER_HUB_CREDENTIALS"
                        docker push your-dockerhub-username/your-image-name:${env.BUILD_NUMBER}
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            // You can add post-build actions here, e.g., sending notifications
        }
    }
}
