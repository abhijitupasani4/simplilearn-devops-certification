pipeline {
    environment {
        registry = "abhijitupasani4/simplilearn-devops-certification"
        registryCredential = 'dockerhub'
        dockerExecutable = "C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe"
        
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
                
                    bat "\"${dockerExecutable}\" rmi ${registry}:${BUILD_NUMBER}"
                }
            }
        }
    }


    node {
        stage('Execute Image') {
                def workspacePath = "${env.WORKSPACE}".replace("\\", "/")
                def customImage = docker.build("abhijitupasani4/simplilearn-devops-certification:${env.BUILD_NUMBER}")
                customImage.inside("-u 1000:1000 -w ${workspacePath}/abhijitupasani4/simplilearn-devops-certification") {
                    sh 'echo This is the code executing inside the container.'
                }
            
        }
    }

