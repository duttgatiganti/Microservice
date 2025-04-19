pipeline {
    agent any

    environment {
        AZURE_SP_APP_ID  = credentials('AZURE_SP_APP_ID')
        AZURE_SP_SECRET  = credentials('AZURE_SP_SECRET')
        AZURE_TENANT_ID  = credentials('AZURE_TENANT_ID')
        AKS_RG           = credentials('AKS_RG')
        AKS_NAME         = credentials('AKS_NAME')
    }

    stages {
        stage('Login to Azure and Get AKS Credentials') {
            steps {
                sh '''
                az login --service-principal \
                  --username "$AZURE_SP_APP_ID" \
                  --password "$AZURE_SP_SECRET" \
                  --tenant "$AZURE_TENANT_ID"

                az aks get-credentials \
                  --resource-group "$AKS_RG" \
                  --name "$AKS_NAME" \
                  --overwrite-existing
                '''
            }
        }

        stage('kubectl test') {
            steps {
                sh 'kubectl get nodes'
            }
        }
    }
}
