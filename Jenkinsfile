
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
                echo 'Source code downloaded successfully'
            }
        }

        stage('Verify Docker') {
            steps {
                bat 'docker version'
                bat 'docker compose version'
            }
        }

        stage('Build and Deploy') {
            steps {
                bat 'docker compose up -d --build'
            }
        }

        stage('Verify Application') {
            steps {
                bat 'docker compose ps'
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
