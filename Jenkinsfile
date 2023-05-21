pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t seansinlao/devops_sean:nginx-devops-v$BUILD_NUMBER .'
      }
    }
    stage('Login') {
  steps {
  sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push seansinlao/devops_sean:nginx-devops-v$BUILD_NUMBER'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}
