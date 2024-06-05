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
                    docker.build("-t ${registry}-auth-service:${BUILD_NUMBER} ./Auth")

                    // Build classroom-service Docker image
                    docker.build("-t ${registry}-classroom-service:${BUILD_NUMBER} ./Classrooms")

                    // Build post-service Docker image
                    docker.build("-t ${registry}-post-service:${BUILD_NUMBER} ./Post")

                    // Build event-bus Docker image
                    docker.build("-t ${registry}-event-bus:${BUILD_NUMBER} ./event-bus")

                    // Build client Docker image
                    docker.build("-t ${registry}-client:${BUILD_NUMBER} ./client")
                }
            }
        }
        stage('Push Docker Images') {
            steps {
                script {
                    // Push auth-service Docker image
                    docker.withRegistry('', DOCKER_CREDENTIALS) {
                        docker.image("${registry}-auth-service:${BUILD_NUMBER}").push()
                    }

                    // Push classroom-service Docker image
                    docker.withRegistry('', DOCKER_CREDENTIALS) {
                        docker.image("${registry}-classroom-service:${BUILD_NUMBER}").push()
                    }

                    // Push post-service Docker image
                    docker.withRegistry('', DOCKER_CREDENTIALS) {
                        docker.image("${registry}-post-service:${BUILD_NUMBER}").push()
                    }

                    // Push event-bus Docker image
                    docker.withRegistry('', DOCKER_CREDENTIALS) {
                        docker.image("${registry}-event-bus:${BUILD_NUMBER}").push()
                    }

                    // Push client Docker image
                    docker.withRegistry('', DOCKER_CREDENTIALS) {
                        docker.image("${registry}-client:${BUILD_NUMBER}").push()
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
