pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "minikube stop"
                sh "minikube start"
                sh "eval `minikube docker-env`"
                sh "kubectl get all"
                sh "docker images"
                sh "docker rmi -f flask-rest"
                sh "docker build -t flask-rest:latest ."
                sh "docker images"
                sh "docker rm `docker container ls -n 1 -q`"
                sh "docker container ls --all"
                sh "docker run -p 8000:8000 -d flask-rest"
                sh "kubectl delete deployment.apps flask-rest"
                sh "kubectl delete service flask-rest-service"
                sh "kubectl apply -f app-deployment.yml"
                sh "sleep 5"
                sh "kubectl get all"
                sh "minikube service list"
            }
        }
    }
}

