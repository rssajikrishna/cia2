pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'web-app:latest'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/rssajikrishna/cia2.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh """
                docker stop web-app || true
                docker rm web-app || true
                docker run -d -p 80:80 --name web-app $DOCKER_IMAGE
                """
            }
        }
    }

    post {
        success {
            echo 'Deployment successful! Your web app should be live.'
        }
        failure {
            echo 'Deployment failed! Check logs for errors.'
        }
    }
}
