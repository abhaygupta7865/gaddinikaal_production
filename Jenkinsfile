pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Build the Docker image from the Dockerfile in the frontend directory
                    sh 'docker build -t frontend ./frontend'
                }
            }
        }

        stage('Run') {
            steps {
                script {
                    // Stop and remove any existing container
                    sh 'docker stop frontend-container || true'
                    sh 'docker rm frontend-container || true'

                    // Run the Docker container
                    sh 'docker run -d --name frontend-container -p 80:80 frontend'
                }
            }
        }
    }

    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
