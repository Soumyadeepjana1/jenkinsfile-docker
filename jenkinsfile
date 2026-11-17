
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
                echo 'Code checked out from GitHub'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cobra-app .'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop cobra-container || true
                    docker rm cobra-container || true

                    docker run -d \
                    --name cobra-container \
                    -p 8080:80 \
                    cobra-app
                '''
            }
        }
    }
}
