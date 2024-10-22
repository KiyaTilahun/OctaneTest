pipeline {

    agent any
    stages {

        stage('Build') {
            steps {
                script {
                    // Run Docker Compose to build and start services
                    sh 'docker-compose -f docker-compose.yml up -d --build'
                }
            }
        }
    }
}
