pipeline {
    agent any

    environment {
        DOCKER_HUB = "mohan118917"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend Image') {
            steps {
                dir('api') {
                    sh "docker build -t ${DOCKER_HUB}/user-management-backend:latest ."
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir('client') {
                    sh "docker build -t ${DOCKER_HUB}/user-management-frontend:latest ."
                }
            }
        }
        stage('Push Images') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub') {
                    sh ''' docker push ${DOCKER_HUB}/user-management-backend:latest
                           docker push ${DOCKER_HUB}/user-management-frontend:latest
                       '''            
                }
            }
        }
    }

        stage('Deploy') {
            steps {
                sh '''
                    docker compose pull
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
