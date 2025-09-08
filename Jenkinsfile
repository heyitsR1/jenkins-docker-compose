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
                echo "Stopping old containers and pruning Docker..."
                // Stop and remove any running containers defined in docker-compose
                sh "${DOCKER_COMPOSE} down"
                // Remove unused Docker data (images, containers, volumes)
                sh 'docker system prune -af --volumes'
            }
        }

        stage('Build & Deploy') {
            steps {
                echo "Building and starting Docker containers..."
                sh "${DOCKER_COMPOSE} up -d --build"
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
