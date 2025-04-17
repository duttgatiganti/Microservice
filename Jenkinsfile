pipeline {       
    agent any

    stages {
        stage('Build & Tag Docker Image2') {
            steps {
                script {
                     
                        sh "docker build -t acr3571.azurecr.io/adservice:latest ."
                    
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'ACR_PASSWORD', usernameVariable: 'ACR_USERNAME')])                    {
                        
                         sh "docker push acr3571.azurecr.io/adservice:latest "
                    }
                }
            }
        }
    }
}
