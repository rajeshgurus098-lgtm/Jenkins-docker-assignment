pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-docker-app"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Build Stage Started...'
                sh 'ls -la'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'
                sh 'test -f index.html'
                echo 'Test Passed'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker Image...'
                sh 'docker build -t ${IMAGE_NAME}:latest .'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
