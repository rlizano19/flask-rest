pipeline {
    agent { docker { image 'alpine:3.1' } }
    stages {
        stage('build') {
            steps {
                sh 'which docker'
                sh 'docker build -t flask-rest .'
            }
        }
        stage('deploy') {
            steps {
                sh 'kubectl apply -f app-deployment.yml'
                sh 'sleep 6'
                sh 'minikube service flask-rest'
            }
        }
    }
}
