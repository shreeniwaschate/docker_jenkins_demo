pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "shreehari208/docker_jenkins_demo"  // Use your Docker Hub username
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:1.0 ."
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(
                        credentialsId: 'docker-hub-credentials',  // Must match Jenkins credentials ID
                        usernameVariable: 'DOCKER_HUB_USER',
                        passwordVariable: 'DOCKER_HUB_PASSWORD'
                    )]) {
                        sh """
                            docker login -u $DOCKER_HUB_USER -p $DOCKER_HUB_PASSWORD
                            docker push ${DOCKER_IMAGE}:1.0
                        """
                    }
                }
            }
        }
    }
}
