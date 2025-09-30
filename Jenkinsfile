pipeline {
  agent any
  environment {
    IMAGE = "yourdockerhubuser/my-docker-app"   // change this to your Docker Hub repo
    CRED_ID = "dockerhub-creds"                 // Jenkins credentials ID
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Build & Push Docker Image') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', CRED_ID) {
            def app = docker.build("${IMAGE}:${BUILD_NUMBER}")
            app.push()
            app.push("latest")
          }
        }
      }
    }
  }
}
