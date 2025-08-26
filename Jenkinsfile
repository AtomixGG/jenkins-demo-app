pipeline {
    agent {
        docker {
            image 'docker:28.0'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AtomixGG/jenkins-demo-app', credentialsId: '18b891b5-0826-49d1-b49d-326b2dafbfb0'
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build --no-cache -t jenkins-demo-app:latest .'
            }
        }
        stage('Run Container') {
            steps {
                sh 'docker rm -f demo-app || true'
                sh 'docker run -d -p 8081:8081 --name demo-app jenkins-demo-app:latest || true'
            }
        }
    }
}
