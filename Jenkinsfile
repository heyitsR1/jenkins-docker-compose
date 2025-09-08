pipeline {
    agent any

    environment {
        DOCKER_COMPOSE = '/usr/local/bin/docker-compose' // adjust path if needed
    }

    stages {
        stage('Check Versions') {
            steps {
                echo "Checking installed versions..."
                sh 'docker --version'
                sh 'docker-compose --version'
                sh 'curl --version'
                sh 'jq --version'
            }
        }

        stage('Clean Docker') {
            steps {
                echo "Pruning unused Docker data..."
                sh 'docker system prune -f'
            }
        }

        stage('Build & Deploy') {
            steps {
                echo "Building and running Docker containers..."
                sh 'docker-compose up -d --build'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for errors.'
        }
    }
}
