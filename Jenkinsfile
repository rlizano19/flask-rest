pipeline {
    stages {
        stage('build') {
            steps {
                which docker
                docker container ls
            }
        }
        stage('deploy') {
            steps {
                sh "eval $(minikube -p minikube docker-env)"
                docker container ls
                docker build -t flask-rest:latest .
                docker run -p 8000:8000 -d flask-rest
                docker image ls
                cat app-deployment.yml
                minikube start
                sleep 6
                kubectl delete deployment.apps/flask-rest
                kubectl delete service/flask-rest-service
                sleep 4
                kubectl get pods,svc,deploy
                kubectl apply -f app-deployment.yml
                sleep 6
                kubectl get pods,svc,deploy
                minikube status
                minikube service flask-rest-service --url
                sleep 60
            }
        }
    }
}
