pipeline {
    agent any

    environment {
        DOCKER_HUB = "mohan118917"
        IMAGE_TAG = "${BUILD_NUMBER}"
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
                    sh "docker build -t ${DOCKER_HUB}/user-management-backend:${IMAGE_TAG} ."
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir('client') {
                    sh "docker build -t ${DOCKER_HUB}/user-management-frontend:${IMAGE_TAG} ."
                }
            }
        }
        stage('Push Images') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub') {
                    sh ''' docker push ${DOCKER_HUB}/user-management-backend:${IMAGE_TAG}
                           docker push ${DOCKER_HUB}/user-management-frontend:${IMAGE_TAG}
                       '''            
                }
            }
        }
    }

        stage('Deploy') {
            steps {
                sh '''
                    echo IMAGE_TAG=${IMAGE_TAG} > .env
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
