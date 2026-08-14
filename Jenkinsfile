pipeline {
    agent any

    environment {
        IMAGE_NAME = "devops-webapp"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub'
                checkout scm
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application'
                bat 'python --version'
                bat 'python -m py_compile app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'
                bat 'docker build -t %IMAGE_NAME%:%IMAGE_TAG% .'
            }
        }

        stage('Verify Docker Image') {
            steps {
                echo 'Checking Docker image'
                bat 'docker images %IMAGE_NAME%:%IMAGE_TAG%'
            }
        }
    }

    post {
        success {
            echo 'Docker build completed successfully!'
        }

        failure {
            echo 'Pipeline failed.'
        }
    }
}