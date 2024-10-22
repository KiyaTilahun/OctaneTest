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
                sh './vendor/bin/sail composer install' // Using Sail to install dependencies
                sh 'cp .env.example .env' // Copy .env example
                sh 'composer install' // Install composer dependencies
                sh 'php artisan key:generate' // Generate application key
            }
        }
        stage('Test') {
            steps {
                // You can add test scripts here, such as PHPUnit tests
                // sh './vendor/bin/sail phpunit'
            }
        }
        stage('Deploy') {
            steps {
                // Add deployment steps here
            }
        }
    }
}
