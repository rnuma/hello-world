pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/<your-username>/flask-ci-cd.git'
        DOCKER_IMAGE = 'yourdockerhub/flask-app'
        DEPLOY_SERVER = 'ec2-user@<your-server-ip>'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: https://github.com/rnuma/hello-world.git, branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $rnuma25/hello-app:latest .'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh '''
                        echo "$Ndungu20012025!" | docker login -u "$rnuma25" --password-stdin
                        docker push $rnuma25/hello-app:latest
                    '''
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    sshagent(['deploy-key']) {
                        sh '''
                            ssh $rnuma@3.145.190.96 "docker pull $rnuma25/hello-app:latest && docker run -d -p 8080:8080 -p 5000:5000 $rnuma25/hello-app:latest"
                        '''
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}