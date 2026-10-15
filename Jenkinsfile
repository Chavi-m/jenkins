```groovy
pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "chavi123/docker-python"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Chavi-m/jenkins.git'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(
                    credentialsId: 'docker-credentials',
                    variable: 'DOCKER_PAT'
                )]) {
                    bat '''
                    @echo off
                    echo %DOCKER_PAT%|docker login -u chavi123 --password-stdin
                    if errorlevel 1 exit /b 1
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %DOCKER_IMAGE%:latest'
            }
        }
    }

    post {
        success {
            echo 'Docker image built and pushed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
```
