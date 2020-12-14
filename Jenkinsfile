pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "minikube start --namespace=dev"
                sh "eval `minikube docker-env`"
                sh "kubectl config set-context dev --namespace=dev --cluster=minikube --user=minikube"
                sh "kubectl config use-context dev"
                sh "kubectl config current-context"
                sh "docker build -t flask-rest-dev:latest ."
                sh "docker images"
            }
        }
        stage('deploy') {
            steps {
                sh "kubectl delete deployment.apps flask-rest"
                sh "kubectl delete service dev-flask-rest-service"
                sh "kubectl get all"
                sh "kubectl apply -f dev-namespace.yml"
                sh "kubectl apply -f app-deployment.yml"
                sh "sleep 5"
                sh "kubectl get all"
                sh "minikube service list"
            }
        }
    }
}

