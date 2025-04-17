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
        stage('Login to ACR') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'acr-admin-creds', // <-- replace with your actual ID
                    usernameVariable: 'ACR_USERNAME',
                    passwordVariable: 'ACR_PASSWORD'
                )]) {
                    sh '''
                    echo "$ACR_PASSWORD" | docker login acr3571.azurecr.io -u "$ACR_USERNAME" --password-stdin
                    '''
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
