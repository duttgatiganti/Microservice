pipeline {
    agent any
    environment {
        K8S_TOKEN = credentials('AKS_TOKEN')
        K8S_API = credentials('AKS_API_SERVER')
    }
   
    }

    stages {
        stage('Setup kubeconfi') {
            steps {
                sh '''
                mkdir -p ~/.kube

                cat > ~/.kube/config <<EOF
apiVersion: v1
kind: Config
clusters:
- cluster:
    server: "$K8S_API"
    insecure-skip-tls-verify: true
  name: aks
contexts:
- context:
    cluster: aks
    user: jenkins
  name: jenkins-context
current-context: jenkins-context
users:
- name: jenkins
  user:
    token: "$K8S_TOKEN"
EOF
                '''
            }
        }

        stage('Apply Deployment') {
            steps {
                sh '''
                echo "Applying deployment.yaml to AKS"
                kubectl apply -f k8smvndeployment.yaml
                '''
            }
        }
    }
}
