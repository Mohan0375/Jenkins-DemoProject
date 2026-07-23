pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend Image') {
            steps {
                dir('api') {
                    sh 'docker build -t user-management-backend:latest .'
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir('client') {
                    sh 'docker build -t user-management-frontend:latest .'
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker compose down || true
                    docker compose up -d
                '''
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }

        always {
            sh 'docker image ls'
            sh 'docker ps -a'
        }
    }
}
