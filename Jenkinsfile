pipeline {
    agent any

    stages {
        stage('Deploy to Kubernetes') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '', 
                    clusterName: 'EKS-1', 
                    contextName: '', 
                    credentialsId: 'k8-token', 
                    namespace: 'webapps', 
                    serverUrl: 'https://648B60D2C5C6A08ED25EBA28B9B97C0A.sk1.eu-west-1.eks.amazonaws.com'
                ]]) {
                    sh "kubectl apply -f deployment-service.yml"
                    sleep 60
                }
            }
        }

        stage('Verify deployment') {
            steps {
                withKubeCredentials(kubectlCredentials: [[
                    caCertificate: '', 
                    clusterName: 'EKS-1', 
                    contextName: '', 
                    credentialsId: 'k8-token', 
                    namespace: 'webapps', 
                    serverUrl: 'https://648B60D2C5C6A08ED25EBA28B9B97C0A.sk1.eu-west-1.eks.amazonaws.com'
                ]]) {
                    sh "kubectl get all -n webapps"
                }
            }
        }
    }
}
