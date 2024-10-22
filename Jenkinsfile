pipeline {
    agent any
    stages {
        stage('Clean workspace') {
            steps {
                deleteDir() // Cleans the workspace
                sh 'ls -lah' // Lists files in the workspace
            }
        }
        stage('Install Composer') {
            steps {
                // Download and install Composer
                sh 'curl -sS https://getcomposer.org/installer | php'
                // Move Composer to a global location
                sh 'mv composer.phar /usr/local/bin/composer'
                // Ensure Composer is executable
                sh 'chmod +x /usr/local/bin/composer'
            }
        }
        stage('Build') {
            steps {
                sh 'composer install' // Install composer dependencies
                sh 'php artisan key:generate' // Generate application key
            }
        }
    }
}
