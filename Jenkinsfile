pipeline {
    agent any

    environment {
        IMAGE_NAME = 'front-web'
        CONTAINER_NAME = 'front_web'
        GIT_REPO = 'https://github.com/VitorMalacarne/TAC_frontEnd.git'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: "${GIT_REPO}"
            }
        }

        stage('Clean old containers/images') {
            steps {
                sh '''
                docker rm -f ${CONTAINER_NAME} || true
                docker rmi -f ${IMAGE_NAME}:latest || true
                '''
            }
        }

        stage('Build image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Run container') {
            steps {
                sh 'docker run -d --name ${CONTAINER_NAME} -p 8081:80 ${IMAGE_NAME}:latest'
            }
        }
    }
}
