pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('stormihein')
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/stormihein/W6D2.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t stormihein/jenkins-lts .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'stormihein', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    sh 'docker push stormihein/jenkins-lts'
                }
            }
        }
    }
}
