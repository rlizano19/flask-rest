pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "minikube start"
                sh "eval `minikube docker-env`"
                sh "kubectl get all"
                sh "docker build -t flask-rest:latest ."
                sh "docker images"
                sh "docker container ls --all"
                sh "kubectl apply -f app-deployment.yml"
                sh "kubectl get all"
                sh "minikube service list"
            }
        }
    }
}
