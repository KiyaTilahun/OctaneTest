pipeline {
    agent any
    stages {
        stage('Clean workspace') {
            steps {
                deleteDir()
                sh 'ls -lah'
            }
        }
        stage('Build') {
            steps {
                // Use a Docker container with PHP and Composer
                script {
                    // Run commands inside a Docker container
                    sh '''
                        docker run --rm \
                        -v $(pwd):/app \
                        -w /app \
                        composer:latest \
                        install
                    '''
                }
                sh 'cp .env.example .env'
                sh 'php artisan key:generate'
            }
        }
        stage('Test') {
            steps {
                // Add your test steps here, you might need to run tests inside the same container
                script {
                    sh '''
                        docker run --rm \
                        -v $(pwd):/app \
                        -w /app \
                        composer:latest \
                        php artisan test
                    '''
                }
            }
        }
        stage('Deploy') {
            steps {
                // Add your deployment steps here, similar to above
                script {
                    sh '''
                        docker run --rm \
                        -v $(pwd):/app \
                        -w /app \
                        composer:latest \
                        php artisan deploy
                    '''
                }
            }
        }
    }
}
