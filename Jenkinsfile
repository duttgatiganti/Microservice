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
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push dutt1/adservice:latest "
                    }
                }
            }
        }
    }
}
