pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "bhagyasree0506/rural-education"
        CONTAINER_NAME = "rural-app"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred-new', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    bat 'docker login -u %USERNAME% -p %PASSWORD%'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                bat 'docker push %DOCKER_IMAGE%'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                docker stop %CONTAINER_NAME% || exit 0
                docker rm %CONTAINER_NAME% || exit 0
                docker run -d -p 8085:80 --name %CONTAINER_NAME% %DOCKER_IMAGE%
                '''
            }
        }
    }
}
