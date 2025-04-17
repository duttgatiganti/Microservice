pipeline {       
    agent any

    environment {
        ACR_NAME = 'acr3571.azurecr.io'
        IMAGE_NAME = 'adservice'
        DOCKER_CREDENTIALS_ID = 'DOCKER_CREDENTIALS_ID' // Jenkins credential ID for Docker login
        IMAGE_TAG = '$BUILD_ID'
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

        stage('Build & Push') {
            steps {
                sh "docker build -t ${ACR_NAME}/${IMAGE_NAME}:${IMAGE_TAG} ."
                sh "docker push ${ACR_NAME}/${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }

        
    }

    
}
