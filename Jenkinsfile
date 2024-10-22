
pipeline {
    agent any
    stages {
        stage('Clean workspace') {
                    deleteDir()
                    sh 'ls -lah'
        }
        stage('Build') {
            steps {
                //
                sh './vendor/bin/sail composer install'
                sh 'cp .env.example .env'
                sh 'composer install'
                sh 'php artisan key:generate'
            }
        }
        stage('Test') {
            steps {
            //
            }
        }
        stage('Deploy') {
            steps {
            //
            }
        }
    }
}

