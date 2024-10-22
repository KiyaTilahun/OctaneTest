pipeline {
    agent {
        dockerContainer {
            image 'ubuntu:20.04'  // Use a base image
        }
    }
    stages {
        stage('Install PHP and Composer') {
            steps {
                script {
                    // Install PHP, Composer, and necessary extensions
                    sh '''
                        apt-get update
                        apt-get install -y software-properties-common curl git unzip
                        add-apt-repository ppa:ondrej/php -y
                        apt-get update
                        apt-get install -y php8.3 php8.3-cli php8.3-fpm php8.3-mbstring php8.3-xml php8.3-bcmath php8.3-mysql
                        
                        # Install Composer
                        curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
                        
                        # Verify installations
                        php --version
                        composer --version
                    '''
                }
            }
        }
        stage('Checkout Code') {
            steps {
                checkout scm  // Checkout the source code from your repository
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
                    cp .env.example .env
                    composer install
                    php artisan key:generate
                '''
            }
        }
        stage('Start Sail and Run Tests') {
            steps {
                // Start Laravel Sail, set up services, and run tests
                sh '''
                    ./vendor/bin/sail up -d
                    ./vendor/bin/sail artisan migrate
                    ./vendor/bin/sail test
                '''
            }
        }
        stage('Final Test') {
            steps {
                // Run Laravel's PHP tests
                sh 'php artisan test'
            }
        }
    }
    post {
        always {
            // Clean up by stopping Sail
            sh './vendor/bin/sail down'
        }
    }
}
