pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "bhagyasree0506/rural-education"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/Bhagyasree-05/Rural-Education.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE% .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                bat 'docker push %DOCKER_IMAGE%'
            }
        }
    }
}
