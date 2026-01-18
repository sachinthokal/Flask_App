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
                sh '''
                    echo "Stopping and removing existing container (if any)"
                    docker stop flask_container || true
                    docker rm flask_container || true

                    echo "Removing old Docker image (if exists)"
                    docker rmi jenkins-flask-app:1.0 || true

                    echo "Building new Docker image"
                    docker build -t jenkins-flask-app:1.0 .
        '''
    }
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
