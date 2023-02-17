pipeline {
    agent any

    stages {
        stage('Checkout Source') {
            steps {
                git url: 'https://github.com/rafaferreira011/pedelogo-catalogo.git', branch: 'main'
            }
        }

        stage('Build Image') {
            steps {
                script { 
                    dockerapp = docker.build("rafaferreira011/api-produto:${env.BUILD_ID}",'-f ./src/Pedelogo.Catalogo.Api/Dockerfile ./src')
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
