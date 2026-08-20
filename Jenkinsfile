pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-docker-app"
        CONTAINER_NAME = "jenkins-docker-container"
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
                sh '/usr/bin/docker build -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Docker Run') {
            steps {
                echo 'Running Docker Container...'

                sh '/usr/bin/docker rm -f ${CONTAINER_NAME} || true'

                sh '/usr/bin/docker run -d --name ${CONTAINER_NAME} -p 8080:80 ${IMAGE_NAME}:latest'

                sh '/usr/bin/docker ps'
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
