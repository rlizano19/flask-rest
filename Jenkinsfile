pipeline {
    agent { docker { image 'alpine:3.1' } }
    stages {
        stage('build') {
            steps {
                docker build -t flask-rest .
            }
        }
        stage('deploy') {
            steps {
                kubectl apply -f app-deployment.yml
                sleep 6
                minikube service flask-rest
            }
        }
    }
}
