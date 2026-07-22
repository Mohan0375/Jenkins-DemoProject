pipeline {
    agent any

    stages {
        stage('Checkout Verification') {
            steps {
                echo 'Repository successfully checked out.'

                sh 'pwd'
                sh 'ls -la'
            }
        }

	stage('Install Backend Dependencies') {
    steps {
        dir('api') {
            sh 'npm install'
         }
        }
      }
    }
}
