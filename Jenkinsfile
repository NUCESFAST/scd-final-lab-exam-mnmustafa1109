pipeline {
    agent any

    environment {
        registry = "mnmustafa1109/scd-lab-final"
        DOCKER_CREDENTIALS = '0eae42a5-0efa-44e8-b82a-fdeea921b6ac'
    }

    stages {
        stage('Build Docker Images') {
            steps {
                script {
                    // Build auth-service Docker image
                    dockerAuth = docker.build registry + ":auth-service-${BUILD_NUMBER}", './Auth'

                    // Build classroom-service Docker image
                    dockerClassroom = docker.build registry + ":classroom-service-${BUILD_NUMBER}", './Classroom'

                    // Build post-service Docker image
                    dockerPost = docker.build registry + ":post-service-${BUILD_NUMBER}", './Post'

                    // Build event-bus Docker image
                    dockerEventBus = docker.build registry + ":event-bus-${BUILD_NUMBER}", './EventBus'

                    // Build client Docker image
                    dockerClient = docker.build registry + ":client-${BUILD_NUMBER}", './Client'
                }
            }
        }
        stage('Push Docker Images') {
            steps {
                script {
                    // Push auth-service Docker image
                   docker.withRegistry('', DOCKER_CREDENTIALS) {
                        // Push the built image to Docker Hub
                        dockerAuth.push()
                        dockerClassroom.push()
                        dockerPost.push()
                        dockerEventBus.push()
                        dockerClient.push()
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
