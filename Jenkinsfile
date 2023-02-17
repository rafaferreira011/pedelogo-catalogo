pipeline {
    agent any

    stages {
        stage('Build Image') {
            steps {
                script { 
                    dockerapp = docker.build("rafaferreira011/api-produto:${env.BUILD_ID}",'-f ./src/ .')
                }
            }
        }
        
        stage('Push Image') {
            steps {
                script { 
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")
                    }                    
                }
            }
        }
    }
}
