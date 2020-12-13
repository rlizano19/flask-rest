pipeline {
    stages {
        stage('build') {
            steps {
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
