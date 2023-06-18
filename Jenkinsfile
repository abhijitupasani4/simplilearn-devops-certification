pipeline {
    environment {
        registry = "abhijitupasani4/simplilearn-devops-certification"
        registryCredential = 'dockerhub'
        dockerExecutable = "C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe"
    }
    agent any
    stages {
        stage('Build Image') {
            steps {
                echo 'Building Docker image...'
                script {
                    dockerImage = docker.build("${registry}:${env.BUILD_NUMBER}")
                }
                echo 'Docker image built successfully.'
            }
        }

        stage('Deploy Image') {
            steps {
                echo 'Deploying Docker image...'
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
                echo 'Docker image deployed successfully.'
            }
        }

        stage('Remove Image') {
            steps {
                echo 'Removing Docker image...'
                script {
                    bat "\"${dockerExecutable}\" rmi ${registry}:${env.BUILD_NUMBER}"
                }
                echo 'Docker image removed successfully.'
            }
        }
    }
}

    node {
        stage('Execute Image') {

                echo 'Executing Docker image...'

                    def customImage = docker.build("${registry}:${env.BUILD_NUMBER}")
                    customImage.inside {
                        sh 'echo This is the code executing inside the container.'
                    }
                }
                echo 'Docker image executed successfully.'
            
        }
    

