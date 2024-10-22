pipeline {
    agent {
        dockerfile {
            filename 'docker-compose'
            dir './'
        }
    }
    stages {
        stage('Test') {
            steps {
                sh 'php --version'
            }
        }
    }
}