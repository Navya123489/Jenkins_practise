pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling code from GitHub...'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'echo Build step - would compile/test here'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                echo 'Deploying to Kubernetes...'
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
        stage('Verify Deployment') {
            steps {
                echo 'Verifying deployment...'
                sh 'kubectl rollout status deployment/jenkins-deployed-app'
                sh 'kubectl get pods'
            }
        }
    }
    post {
        success {
            echo 'Deployment successful!'
            sh 'kubectl get services jenkins-deployed-app'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
