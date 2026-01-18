pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-flask-app:1.0 .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8000:8000 jenkins-flask-app:1.0'
            }
        }
    }

    post {
        success {
            echo 'Docker Pipeline SUCCESS 🎉'
        }
        failure {
            echo 'Docker Pipeline FAILED ❌'
        }
    }
}
