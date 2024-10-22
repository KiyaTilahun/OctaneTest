pipeline {
    agent any
    environment {
        SAIL_CMD = './vendor/bin/sail' // Command to run Sail
        DOCKER_COMPOSE_CMD = 'docker-compose'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the source code from your Git repository
                git branch: 'master',  url: 'git@github.com:your-username/your-repo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Laravel dependencies via Composer
                sh "${SAIL_CMD} composer install"
            }
        }

        stage('Run Tests') {
            steps {
                // Run your Laravel PHPUnit tests
                sh "${SAIL_CMD} test"
            }
        }

        stage('Build Docker Containers') {
            steps {
                // Build the Sail containers (optional)
                sh "${DOCKER_COMPOSE_CMD} up -d --build"
            }
        }

        stage('Deploy Application') {
            steps {
                // Define steps to deploy the Laravel application to a server (e.g., SCP, FTP, or deployment script)
                echo "Deploying Application"
            }
        }
    }

    post {
        always {
            // Archive logs, clean up, etc.
            archiveArtifacts artifacts: '**/storage/logs/*.log', allowEmptyArchive: true
            cleanWs()
        }
    }
}
