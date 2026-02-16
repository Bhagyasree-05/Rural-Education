pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "bhagyasree0506/rural-education"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    bat 'docker login -u %USERNAME% -p %PASSWORD%'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                bat 'docker push %DOCKER_IMAGE%'
            }
        }
    }
}
