pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t abhijitupasani4/simplilearn-devops-certification:${env.BUILD_NUMBER} .'
        echo "Building Docker Image"
      }
    }

    stage('Push Docker Image') {
      steps {
        sh 'docker push abhijitupasani4/simplilearn-devops-certification:${env.BUILD_NUMBER}'
        echo "Pushing Docker Image"
      }
    }

    stage('Run Docker Container') {
      steps {
        sh 'docker run -d -p 8080:3000 --name my-container abhijitupasani4/simplilearn-devops-certification:${env.BUILD_NUMBER}'
        echo "Running Docker Container"
      }
    }
  }
}
