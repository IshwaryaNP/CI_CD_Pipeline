pipeline {
    agent any

    environment {
        DOCKER = 'C:\\Users\\Ishwarya\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe'
    }

    stages {
        stage('Docker Version') {
            steps {
                bat '"%DOCKER%" --version'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '"%DOCKER%" build --no-cache -t vite-app .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                "%DOCKER%" stop vite-container
                "%DOCKER%" rm vite-container
                "%DOCKER%" run -d -p 8081:80 --name vite-container vite-app
                '''
            }
        }
    }
}
