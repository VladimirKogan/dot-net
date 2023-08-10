pipeline {
    agent {
        label 'jenkins-pod'
    }

    environment {
        DOCKER_IMAGE = 'vladimirkogan/dotnet-simple'
        DOCKER_TAG = 'latest'
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Войдите в Docker реестр
                    docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                        docker.image("${DOCKER_IMAGE}:${DOCKER_TAG}").push()
                    }
                }
            }
        }
    }
}
