pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh "git checkout $ENVIRONMENT"
                sh "git status"
                sh "minikube start --namespace=$ENVIRONMENT"
                sh "eval `minikube docker-env`"
                sh "kubectl config set-context $ENVIRONMENT --namespace=$ENVIRONMENT --cluster=minikube --user=minikube"
                sh "kubectl config use-context $ENVIRONMENT"
                sh "kubectl config current-context"
                sh "docker build -t flask-rest-$ENVIRONMENT:latest ."
                sh "docker images"
            }
        }
        stage('deploy') {
            steps {
                sh "kubectl get all"
                sh "kubectl apply -f $ENVIRONMENT-namespace.yml"
                sh "kubectl apply -f app-deployment.yml"
                sh "sleep 5"
                sh "kubectl get all"
                sh "minikube service list"
            }
        }
    }
}

