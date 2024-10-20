pipeline {
    agent any

    stages {
        stage('Test Docker') {
            steps {
                script {
                    sh 'docker --version' // Check Docker version
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build the Docker image from the Dockerfile in the frontend directory
                    sh 'docker build -t frontend .'
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
                    sh 'docker run -d --name frontend-container -p 8081:8081 frontend'
                }
            }
        }
    }

    post {
        always {
            script {
                echo 'This will always run'
            }
        }
        success {
            script {
                echo 'Build and deployment successful!'
            }
        }
        failure {
            script {
                echo 'Build failed!'
            }
        }
    }
}
