pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('greatcoder')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/ravdy/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t greatcoder/nodeapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS| docker login -u $DOCKERHUB_CREDENTIALS --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push greatcoder/nodeapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

