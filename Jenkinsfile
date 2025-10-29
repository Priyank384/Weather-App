pipeline {
    agent any   
    environment {
        IMAGE_NAME = "my-weather-app:latest"
        KUBECONFIG = "/var/lib/jenkins/.kube/config" 
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Priyank384/Weather-App.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Deploy to K3s') {
            steps {
                echo "Deploying application to K3s..."
                sh """
                    kubectl apply -f deployment.yaml
                    kubectl apply -f service.yaml
                    kubectl rollout status deployment/my-weather-app
                """
            }
        }
    }

    post {
        success {
            echo '✅ Deployment succeeded!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
