pipeline {
  agent any
  
  environment {
    registry = "abhijitupasani4/simplilearn-devops-certification"
    registryCredential = 'dockerhub'
  }
  
  stages {
    stage('Build Image') {
      steps {
        script {
          docker.image().build(registry + ":$BUILD_NUMBER")
        }
      }
    }
    
    stage('Push Image') {
      steps {
        script {
          docker.withRegistry('', registryCredential) {
            docker.image(registry + ":$BUILD_NUMBER").push()
          }
        }
      }
    }
    
    stage('Remove Image') {
      steps {
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
    
    stage('Execute Image') {
      agent {
        docker {
          image registry + ":$BUILD_NUMBER"
        }
      }
      steps {
        sh 'echo This is the code executing inside the container.'
      }
    }
  }
}
