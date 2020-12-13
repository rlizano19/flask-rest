pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "docker container ls"
                sh "docker build -t flask-rest:latest ."
            }
        }
        stage('deploy') {
            steps {
                sh "eval `minikube docker-env`"
                sh "docker container ls"
                sh "docker run -p 8000:8000 -d flask-rest"
                sh "minikube status"
                sh "minikube start"
                sh "sleep 6"
                sh "kubectl delete deployment.apps/flask-rest"
                sh "kubectl delete service/flask-rest-service"
                sh "sleep 4"
                sh "kubectl get pods,svc,deploy"
                sh "kubectl apply -f app-deployment.yml"
                sh "sleep 6"
                sh "kubectl get pods,svc,deploy"
                sh "minikube service flask-rest-service --url"
            }
        }
    }
}
