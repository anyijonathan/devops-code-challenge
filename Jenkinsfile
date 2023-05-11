pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', 
                          branches: [[name: 'main']], 
                          userRemoteConfigs: [[url: 'https://github.com/anyijonathan/devops-code-challenge.git']]])
            }
        }
        
        stage('Build') {
            steps {
                sh 'docker-compose build'
            }
        }
        
        stage('Test') {
            steps {
                sh 'docker-compose run --rm backend npm test'
            }
        }
        
        stage('Push to AWS Container Registry') {
            steps {
                withCredentials([string(credentialsId: 'aws-creds', variable: 'AWS_ACCESS_KEY_ID'), 
                                  string(credentialsId: 'aws-creds', variable: 'AWS_SECRET_ACCESS_KEY'), 
                                  string(credentialsId: 'aws-creds', variable: 'AWS_DEFAULT_REGION')]) {
                    sh 'eval $(aws ecr get-login --no-include-email)'
                    sh 'docker tag your-image-name:latest aws-account-id.dkr.ecr.aws-region.amazonaws.com/your-image-name:latest'
                    sh 'docker push aws-account-id.dkr.ecr.aws-region.amazonaws.com/your-image-name:latest'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
