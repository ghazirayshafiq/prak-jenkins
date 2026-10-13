pipeline {
    agent any
    environment {
        IMAGE_NAME = 'ghazirayshafiq/simple-app'
        REGISTRY_CREDENTIALS = credentials('dockerhub-credentials')
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Melakukan checkout dari SCM...'
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Mulai build aplikasi'
                bat 'echo "Build selesai ✅"'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Membangun Docker image...'
                bat "docker build -t %IMAGE_NAME%:%BUILD_NUMBER% -t %IMAGE_NAME%:latest ."
                echo "Image berhasil dibuat: ${IMAGE_NAME}:${env.BUILD_NUMBER}"
            }
        }
        stage('Push Docker Image') {
            steps {
                echo 'Push image ke Docker Hub...'
                bat """
                    docker login -u %REGISTRY_CREDENTIALS_USR% -p %REGISTRY_CREDENTIALS_PSW%
                    docker push %IMAGE_NAME%:%BUILD_NUMBER%
                    docker push %IMAGE_NAME%:latest
                    docker logout
                """
            }
        }
    }
    post {
        always {
            echo 'Selesai build 🏁OYYY'
        }
    }
}
