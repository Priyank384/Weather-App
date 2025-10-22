pipeline {
    agent any
    environment {
        IMAGE_NAME = "weather-app:latest"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Priyank384/Weather-App.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Deploy to k3s') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
                sh 'kubectl rollout status deployment/weather-app'
            }
        }
    }
    post {
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
