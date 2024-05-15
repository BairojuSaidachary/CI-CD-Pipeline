pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY_URL = 'docker.io'
        DOCKER_REPOSITORY = 'saidachary/first-application'
        DOCKER_CREDENTIALS_ID = 'docker-hub-creds'
        DOCKER_IMAGE_NAME = 'sample-image'
        DOCKER_IMAGE_TAG = 'lastest'
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from your version control system (e.g., Git)
                git branch: 'main', url: 'https://github.com/BairojuSaidachary/CI-CD.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Build the Docker image
                sh 'docker build -t $DOCKER_IMAGE_NAME .'
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                // Retrieve Docker Hub credentials from Jenkins credentials
                withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS_ID, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    // Log in to Docker Hub
                    sh "echo \$DOCKER_PASSWORD | docker login -u \$DOCKER_USERNAME --password-stdin \$DOCKER_REGISTRY_URL"
                    
                    // Tag the Docker image
                    sh "docker tag $DOCKER_IMAGE_NAME $DOCKER_REGISTRY_URL/$DOCKER_REPOSITORY:$DOCKER_IMAGE_TAG"
                    
                    // Push the Docker image to Docker Hub
                    script {
                        def pushResult = sh(returnStatus: true, script: "docker push $DOCKER_REGISTRY_URL/$DOCKER_REPOSITORY:$DOCKER_IMAGE_TAG")
                        if (pushResult != 0) {
                            error 'Failed to push Docker image to Docker Hub'
                        }
                    }
                }
            }
        }
    }
}
