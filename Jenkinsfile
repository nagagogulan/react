pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout your code from a version control system (e.g., Git)
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node.js and npm dependencies
                sh "npm install"
            }
        }

        stage('Build') {
            steps {
                // Build your React app
                sh "npm run build"
            }
        }

        stage('Deploy') {
            steps {
                // You can define your deployment steps here
                // For example, copying files to a web server, deploying to AWS, or using Docker
            }
        }
    }

    post {
        success {
            // You can add post-build actions here, e.g., sending notifications
        }
    }
}
