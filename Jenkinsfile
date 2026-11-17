
pipeline {
    agent any

    environment {
        DOCKER_COMPOSE = 'C:\\Users\\sankar\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker-compose.exe'
    }

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code downloaded successfully'
            }
        }

        stage('Verify Docker') {
            steps {
                bat 'docker version'
                bat '"%DOCKER_COMPOSE%" version'
            }
        }

        stage('Build and Deploy') {
            steps {
                bat '"%DOCKER_COMPOSE%" up -d --build'
            }
        }

        stage('Verify Application') {
            steps {
                bat '"%DOCKER_COMPOSE%" ps'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
            echo 'Application: http://localhost:8000/todos'
        }

        failure {
            echo 'Pipeline failed. Check Console Output.'
        }
    }
}
