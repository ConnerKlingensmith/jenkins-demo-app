pipeline {
    agent any

    environment {
        IMAGE_NAME = "connerklingensmith/jenkins-demo-app"
    }

    stages {
        stage("Build Docker Image") {
            steps {
                script {
                    // Use Docker Pipeline plugin to build image
                    dockerImage = docker.build("${IMIAGE_NAME}:${BUILD_NUMBER}")
                }
            }
        }
        
        stage("push to Docker Hub") {
            steps {
                script {
                    // Use DOcker Pipeline to push with credentials
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        dockerImage.push("${BUILD_NUMBER}")
                        dockerImage.push("latest")
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded! Image pushed: ${IMAGE_NAME}:${BUILD_NUMBER}"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}

