pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub') // Replace with your Jenkins credential ID
        IMAGE_NAME = "bhagyasree0506/rural-education"
        KUBE_CONFIG = credentials('kubeconfig') // optional if you use local kubeconfig
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Bhagyasree-05/Rural-Education.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    bat "docker login -u %USERNAME% -p %PASSWORD%"
                    bat "docker push ${IMAGE_NAME}:latest"
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                // Apply deployment and service YAML
                bat "kubectl apply -f k8s/deployment.yaml"
                bat "kubectl apply -f k8s/service.yaml"

                // Optional: rollout restart to update pods with latest image
                bat "kubectl rollout restart deployment rural-education-deployment"
            }
        }
    }
}
