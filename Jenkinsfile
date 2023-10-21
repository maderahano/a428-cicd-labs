pipeline {
    agent {
        docker {
            image 'node:16-buster-slim' 
            args '-p 3000:3000' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approve') {
            steps {
                input message: 'Procesd to the Deploy Stage? (Click "Proceed" to end it)'
            }
        }
       stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Proceed to kill the server React App? (Click "Proceed" to end it)'
                sh 'sleep 1m'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}