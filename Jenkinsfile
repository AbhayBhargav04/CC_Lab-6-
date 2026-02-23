pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend Image') {
            steps {
                sh 'docker rmi -f backend-app || true'
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Deploy Backend Container') {
            steps {
                sh 'docker rm -f backend || true'
                sh 'docker run -d --name backend --network app-network backend-app'
            }
        }

        stage('Build NGINX Image') {
            steps {
                sh 'docker rmi -f nginx-app || true'
                sh 'docker build -t nginx-app nginx'
            }
        }

        stage('Deploy NGINX Container') {
            steps {
                sh 'docker rm -f nginx || true'
                sh 'docker run -d --name nginx --network app-network -p 8081:80 nginx-app'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed. Check console logs for errors.'
        }
        success {
            echo 'Pipeline executed successfully.'
        }
    }
}
