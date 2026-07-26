pipeline {
    agent any

    stages {

        stage('checkout') {
            steps {
                echo 'cloning Github repository...'
                checkout scm 
            }
        }
        stage('verify') {
            steps {
                sh 'pwd'
                sh 'ls -la'
            }
        }
    }
}