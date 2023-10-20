pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("nagagogulan/nodejs-app:${env.BUILD_ID}")
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                script {
                    dockerImage.push()
                }
            }
        }
    }
    
    post {
        always {
            script {
                dockerImage.remove()
            }
        }
    }
}
