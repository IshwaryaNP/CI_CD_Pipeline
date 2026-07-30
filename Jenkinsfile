pipeline {
    agent any

    stages {

        stage('Debug Environment') {
            steps {
                bat '''
                echo ===== Current User =====
                whoami

                echo.
                echo ===== Current Directory =====
                cd

                echo.
                echo ===== PATH =====
                echo %PATH%

                echo.
                echo ===== Docker Location =====
                where docker

                echo.
                echo ===== Docker Version =====
                docker --version

                echo.
                echo ===== Docker Info =====
                docker info
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '''
                docker build --no-cache -t vite-app .
                '''
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                docker stop vite-container 2>nul
                docker rm vite-container 2>nul

                docker run -d -p 8081:80 --name vite-container vite-app
                '''
            }
        }
    }

    post {
        always {
            echo "Pipeline Finished"
        }
        success {
            echo "Docker image built and container deployed successfully."
        }
        failure {
            echo "Pipeline failed. Check the debug output above."
        }
    }
}
