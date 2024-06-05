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
                    // Define dockerImages inside the script block
                    def dockerImages = ['auth-service', 'classroom-service', 'post-service', 'event-bus', 'client']

                    // Loop through each service and build Docker image
                    dockerImages.each { service ->
                        def imageTag = "${registry}-${service}:${BUILD_NUMBER}"
                        docker.build("-t ${imageTag} ./path/to/${service}")
                    }
                }
            }
        }
        stage('Push Docker Images') {
            steps {
                script {
                    def dockerImages = ['auth-service', 'classroom-service', 'post-service', 'event-bus', 'client']
                    dockerImages.each { service ->
                        def imageTag = "${registry}-${service}:${BUILD_NUMBER}"
                        docker.withRegistry('', DOCKER_CREDENTIALS) {
                            // Push the built image to Docker Hub
                            docker.image("${imageTag}").push()
                        }
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
