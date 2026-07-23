pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Repository successfully checked out.'
            }
        }

        stage('Install Backend Dependencies') {
            steps {
                dir('api') {
                    sh 'node -v'
                    sh 'npm -v'
                    sh 'npm install'
                }
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir('client') {
                    sh 'node -v'
                    sh 'npm -v'
                    sh 'npm install'
                }
            }
        }
    }
}

