pipeline {
    agent any
    triggers {
        pollSCM('H/5 * * * *') // every 5 minutes
    }
    environment {
        IMAGE_NAME = "devops-app"
        CONTAINER_NAME = "devops-container"
        APP_PORT = "5000"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                bat "docker build --no-cache -t %IMAGE_NAME% ."
            }
        }
        stage('Stop Existing Container') {
            steps {
                bat '''
                docker stop %CONTAINER_NAME% || echo "No container to stop"
                docker rm %CONTAINER_NAME% || echo "No container to remove"
                '''
            }
        }
        stage('Run New Container') {
            steps {
                bat "docker run -d --name %CONTAINER_NAME% -p %APP_PORT%:%APP_PORT% %IMAGE_NAME%"
            }
        }
    }
}