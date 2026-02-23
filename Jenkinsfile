pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend Image') {
            steps {
                sh '''
                cd backend
                docker build -t backend-app .
                '''
            }
        }

        stage('Run Backend Container') {
            steps {
                sh '''
                docker rm -f backend || true
                docker run -d --name backend backend-app
                '''
            }
        }

        stage('Build NGINX Image') {
            steps {
                sh '''
                cd nginx
                docker build -t nginx-app .
                '''
            }
        }

        stage('Run NGINX Container') {
            steps {
                sh '''
                docker rm -f nginx || true
                docker run -d -p 8081:80 --name nginx nginx-app
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}
