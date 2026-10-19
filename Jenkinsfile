pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Frontend') {
            steps {
                sh '''
                    docker build \
                      -t event-booking-frontend:${BUILD_NUMBER} \
                      --build-arg VITE_API_URL="http://15.206.165.230:5000/api" \
                      ./client
                '''
            }
        }

        stage('Build Backend') {
            steps {
                sh '''
                    docker build \
                      -t event-booking-backend:${BUILD_NUMBER} \
                      ./server
                '''
            }
        }
    }

    post {
        success {
            echo 'Both Docker images built successfully.'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
