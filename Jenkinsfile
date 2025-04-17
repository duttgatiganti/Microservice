pipeline {       
    agent any

    environment {
        ACR_NAME = 'acr3571.azurecr.io'
        IMAGE_NAME = 'adservice'
        DOCKER_CREDENTIALS_ID = credientials(DOCKER_CREDENTIALS_ID) // Jenkins credential ID for Docker login
        IMAGE_TAG = 'latest'
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

        stage('Build & Tag Docker Image') {
            steps {
                sh "docker build -t ${ACR_NAME}/${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push ${ACR_NAME}/${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
    }

    
}
