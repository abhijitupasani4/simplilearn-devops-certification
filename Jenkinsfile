pipeline {
    environment {
        registry = "abhijitupasani4/simplilearn-devops-certification"
        registryCredential = 'dockerhub'
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
                sh "C:\\Program Files\\Docker\\docker.exe rmi ${registry}:${BUILD_NUMBER}"
            }
        }

        stage('Execute Image') {
            steps {
                node {
                    script {
                        def customImage = docker.build("${registry}:${env.BUILD_NUMBER}")
                        customImage.inside {
                            sh 'echo This is the code executing inside the container.'
                        }
                    }
                }
            }
        }
    }
}
