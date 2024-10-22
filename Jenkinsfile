pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm  // Checkout the source code
            }
        }
        stage('Set Up PHP') {
            steps {
                script {
                    // Set up PHP and install required extensions
                    sh '''
                        curl -sSL https://raw.githubusercontent.com/shivammathur/setup-php/master/setup.sh | bash
                        setup-php --version 8.3 --extensions mbstring,pdo,xml,bcmath
                    '''
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                // Set up .env file and install Composer dependencies
                sh '''
                    cp .env.example .env
                    composer install
                    php artisan key:generate
                '''
            }
        }
        stage('Start Sail and Run Tests') {
            steps {
                // Start Sail and run tests
                sh '''
                    ./vendor/bin/sail up -d
                    ./vendor/bin/sail composer require laravel/octane spiral/roadrunner-cli spiral/roadrunner-http
                    ./vendor/bin/sail shell -c "./vendor/bin/rr get-binary"
                    ./vendor/bin/sail build --no-cache
                    ./vendor/bin/sail artisan migrate
                    ./vendor/bin/sail test
                '''
            }
        }
        stage('Final Test') {
            steps {
                // Final testing stage
                sh 'php artisan test'
            }
        }
    }
    post {
        always {
            // Cleanup actions or notifications can go here
            sh './vendor/bin/sail down'  // Stop Sail if running
        }
    }
}
