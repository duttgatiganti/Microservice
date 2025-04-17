pipeline {       
    agent any

    stages {
        stage('Build & Tag Docker Image2') {
            steps {
                script {
                     
                        sh "docker build -t dutt1/adservice:latest ."
                    
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
withCredentials([usernamePassword(credentialsId: 'docker-cred', passwordVariable: 'ACR_PASSWORD', usernameVariable: 'ACR_USERNAME')])                    {
                        
                         sh "docker push dutt1/adservice:latest "
                    }
                }
            }
        }
    }
}
