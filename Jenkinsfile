pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Manually check out your Git repository
                git url: 'your-repository-url', branch: 'your-branch'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build and Run') {
            steps {
                sh 'npm start'
            }
        }
    }

    post {
        success {
            echo 'Node.js application build and run were successful!'
        }
        failure {
            echo 'Node.js application build or run failed.'
        }
    }
}

