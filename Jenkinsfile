pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('jona-jenkins')
  }
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
        bat 'docker-compose'
      }
    }
    stage('Login') {
      steps {
        bat 'echo %DOCKERHUB_CREDENTIALS_PSW% | docker login -u %DOCKERHUB_CREDENTIALS_USR% --password-stdin'
      }
    }
    stage('Push') {
      steps {
        bat 'docker push lloydmatereke/jenkins-docker-hub'
      }
    }
  }
  post {
    always {
      bat 'docker logout'
    }
  }
}
