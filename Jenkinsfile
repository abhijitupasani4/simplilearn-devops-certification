pipeline {
  environment {
    registry = "abhijitupasani4/simplilearn-devops-certification"
    registryCredential = 'dockerhub'
  }
  agent any
  stages {
        stage('Building image') {
        steps{
            script {
            dockerImage = docker.build registry + ":$BUILD_NUMBER"
            }
        }
        }

        stage('Deploy Image') {
        steps{
            script {
            docker.withRegistry( '', 'dockerhub' ) {
                dockerImage.push()
            }
            }
        }
        }

        stage('Remove Image') {
        steps{
            bat "docker rmi $registry:$BUILD_NUMBER"
        }
        }


        stage('Execute Image'){
        def customImage = docker.build("abhijitupasani4/simplilearn-devops-certification:${env.BUILD_NUMBER}")
        customImage.inside {
            sh 'echo This is the code executing inside the container.'
        }
    }
   }   
}

// node {
//     stage('Execute Image'){
//         def customImage = docker.build("abhijitupasani4/simplilearn-devops-certification:${env.BUILD_NUMBER}")
//         customImage.inside {
//             sh 'echo This is the code executing inside the container.'
//         }
//     }
// }