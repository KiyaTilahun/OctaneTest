
pipeline {
    agent {
        dockerContainer { image 'composer:latest' }
    }
    stages {
        stage('Test') {
            steps {
                sh 'composer --version'
            }
        }
    }
}