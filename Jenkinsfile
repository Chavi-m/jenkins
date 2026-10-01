pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "chavi123/docker-python"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/Chavi-m/jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-creds') {
                        docker.image("${DOCKER_IMAGE}:latest").push()
                    }
                }
            }
        }
    }
}