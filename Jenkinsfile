pipeline {       
    agent any
    environment {
        ACR_NAME = 'acr3571.azurecr.io'
        IMAGE_NAME = 'adservice'
        DOCKER_CREDENTIALS_ID = 'acr-docker-creds'  // Jenkins credential ID for Docker login
        AZURE_CREDENTIALS_ID = 'acr-azure-json'     // Jenkins credential ID for Azure JSON
    }

    stages {
        stage('Login to ACR') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "${DOCKER_CREDENTIALS_ID}",
                    usernameVariable: 'ACR_USERNAME',
                    passwordVariable: 'ACR_PASSWORD'
                )]) {
                    sh "echo $ACR_PASSWORD | docker login $ACR_NAME -u $ACR_USERNAME --password-stdin"
                }
            }
        }
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
