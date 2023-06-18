pipeline {
    environment {
        registry = "abhijitupasani4/simplilearn-devops-certification"
        registryCredential = 'dockerhub'
        dockerExecutable = "C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe"
        workspaceDir = "C:\\Users\\Asus\\.jenkins\\workspace\\simplilearn-devops-certification"
    }
    agent any
    stages {
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Deploy Image') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub') {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Remove Image') {
            steps {
                dir(workspaceDir) {
                    bat "\"${dockerExecutable}\" rmi ${registry}:${BUILD_NUMBER}"
                }
            }
        }
        
        stage('Execute Image') {
            steps {
                script {
                    dir(workspaceDir) {
                        sh "docker run -v ${workspaceDir}:${workspaceDir} -w ${workspaceDir} ${registry}:${BUILD_NUMBER} echo 'This is the code executing inside the container.'"
                    }
                }
            }
        }
    }
}


    // node {
    //     stage('Execute Image') {

    //             def customImage = docker.build("abhijitupasani4/simplilearn-devops-certification:${env.BUILD_NUMBER}")
    //             customImage.inside {
    //                 sh 'echo This is the code executing inside the container.'
    //             }
            
    //     }
    

