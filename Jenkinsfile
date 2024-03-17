pipeline {
    agent any 
    environment {
    dockerhubcreden = credentials('greatcoder')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/ravdy/nodejs-demo.git'
            }
        }
        stage('Build docker image') {
            steps {  
                sh 'docker build -t greatcoderhyd/nodeapppp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $dockerhubcreden_PSW | docker login -u $dockerhubcreden_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push greatcoderhyd/nodeapppp:$BUILD_NUMBER'
            }
        }



        
    stage('Deploy') {
            steps {
                // Deploy Docker container using the built image
                sh 'docker run -d  --name cont1 -p 8080:3000 greatcoderhyd/nodeapppp'
            }
        }

post {
        always {
            // Cleanup after deployment
            sh 'docker rm -f cont1 || true'
        }
    }
    
    
    post {
        always {
            sh 'docker logout'
        }
    }
}
}
