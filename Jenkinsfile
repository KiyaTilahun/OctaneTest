pipeline {
    agent any
    stages {
        stage('Clean workspace') {
            steps {
                deleteDir() // Cleans the workspace
                sh 'ls -lah' // Lists files in the workspace
            }
        }
        stage('Build') {
            steps {
 
                sh 'cp .env.example .env' // Copy .env example
                sh 'composer install' // Install composer dependencies
                sh 'php artisan key:generate' // Generate application key
            }
        }
    }
}
