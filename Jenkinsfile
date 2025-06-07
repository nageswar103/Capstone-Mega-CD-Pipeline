pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/nageswar103/Capstone-Mega-CD-Pipeline.git'
            }  
        }

        stage('Deploy to Kubernetes') {
            steps {
                withKubeConfig(
                    credentialsId: 'k8s-cred',
                    clusterName: 'capstone-cluster',
                    namespace: 'webapps',
                    restrictKubeConfigAccess: false,
                    serverUrl: 'https://EA7E16D489B3410B950F14083635F31D.gr7.ap-south-1.eks.amazonaws.com'
                ) {
                    sh 'kubectl apply -f kubernetes/Manifest.yaml -n webapps'
                    sh 'kubectl apply -f kubernetes/HPA.yaml'
                    sleep 30
                    sh 'kubectl get pods -n webapps'
                    sh 'kubectl get svc -n webapps'
                }
            }  
        }
    }
}
