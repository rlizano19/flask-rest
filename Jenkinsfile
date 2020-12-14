pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "minikube start --namespace=dev"
                sh "eval `minikube docker-env`"
                sh "docker build -t flask-rest:dev ."
                sh "docker images"
            }
        }
        stage('deploy') {
            steps {
                sh "kubectl apply -f dev-namespace.yml"
                sh "kubectl apply -f app-deployment.yml"
                sh "sleep 5"
                sh "kubectl get all"
                sh "minikube service list"
            }
        }
    }
}

