pipeline {
    agent any

    environment {
        // Define your environment variables, such as Docker Hub credentials
        DOCKER_HUB_USERNAME = credentials('nagagogulan')
        DOCKER_HUB_PASSWORD = credentials('Gokul28@@')
    }

    stages {
        stage('https://github.com/nagagogulan/react') {
            steps {
                // Clone your Git repository
                checkout scm
            }
        }

        stage('Build and Package React App') {
            steps {
                // Install Node.js and dependencies
                sh 'npm install'
                sh 'npm run build'  // Adjust the script to build your React app

                // Copy the build files to a separate directory for Docker
                sh 'mkdir -p docker-build'
                sh 'cp -r build/* docker-build/'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def imageName = 'demo'
                    def imageTag = 'latest'
                    def dockerfile = 'Dockerfile'  // Specify the path to your Dockerfile

                    // Build the Docker image
                    sh "docker build -t ${imageName}:${imageTag} -f ${dockerfile} ."
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    def imageTag = 'latest'

                    // Log in to Docker Hub
                    sh "docker login -u ${DOCKER_HUB_USERNAME} -p ${DOCKER_HUB_PASSWORD}"

                    // Push the Docker image to Docker Hub
                    sh "docker push ${imageName}:${imageTag}"
                }
            }
        }
    }

    post {
        success {
            // Cleanup, logout from Docker Hub
            sh "docker logout"
        }
    }
}
