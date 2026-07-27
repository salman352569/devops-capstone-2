pipeline {
    agent any

    environment {
        IMAGE_NAME = "webiste"
        IMAGE_TAG = "v1"
    }

    stages {
        
        stage('checkout') {
            steps {
                checkout scm
            }
        }
    }

    stage('Verify Workspace') {
        steps {
            sh 'pwd'
            sh 'ls -la'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
        }
    }

    stage('Verify Docker Image') {
        steps {
            sh 'docker images | grep website'
        }
    }
}