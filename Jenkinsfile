pipeline {
    agent any

    environment {
        IMAGE_NAME = "webiste"
        IMAGE_TAG = "v1"
    }

    stages {
        
        stage('Checkout') {
            steps {
                checkout scm
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

     stage('Verify Docker Login') {
        steps {
            withCredentials([
                usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'

                )
            ]){
                sh ''' 
                echo "$DOCKER_PASS" | docker login -u "DOCKER_USER" --password-stdin
                '''
            }
        }
     }
     stage('Push Docker Image') {
        steps {
            sh '''
            docker push $IMAGE_NAME:IMAGE_TAG
            '''
        }
     }
    }
    post {
        success {
            echo "Docker Image successfully Pushed"
        }
        failed {
            echo "pipeline Failed"
        }
    }
}