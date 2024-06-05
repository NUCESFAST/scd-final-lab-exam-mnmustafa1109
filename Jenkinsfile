pipeline {
    agent any

     environment {
         registry = "mnmustafa1109/scd-lab-final"
        DOCKER_CREDENTIALS ='0eae42a5-0efa-44e8-b82a-fdeea921b6ac'
        dockerImage = ''
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    // Login to Docker Hub
                    docker.withRegistry('', DOCKER_CREDENTIALS) {
                        // Push the built image to Docker Hub
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Deploy using Docker Compose
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            // Cleanup
            script {
                // Stop and remove containers after use
                sh 'docker-compose down'
            }
        }
    }
}