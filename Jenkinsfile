
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/rnuma/hello-world.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t rnuma25/hello:latest .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    bat 'echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin'
                    bat 'docker push rnuma25/hello:latest'
                    bat 'docker logout'
                }
            }
        }
    }
}
