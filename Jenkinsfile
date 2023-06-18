pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean install'
            }
        }
        
        stage('Docker Build') {
            steps {
                echo 'Building the Docker image...'
                script {
                    def dockerImage = docker.build('simplilearn-dockerization')
                }
            }
        }
        
        stage('Docker Push') {
            steps {
                echo 'Pushing the Docker image to Docker Hub...'
                script {
                    withDockerRegistry([credentialsId: '', url: 'https://registry.hub.docker.com']) {
                        dockerImage.push()
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                sh 'docker run -d simplilearn-dockerization'
            }
        }
    }
}
