pipeline {
    agent any

    environment {
        COMPOSE_FILE = 'docker-compose.yml'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Pulling latest code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Docker images...'
                sh 'docker compose build'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Starting containers...'
                sh 'docker compose up -d'
            }
        }

    }

    post {
        success {
            echo 'Pipeline succeeded! App is running.'
        }
        failure {
            echo 'Pipeline failed. Check the logs above.'
            sh 'docker compose down'
        }
    }
}
