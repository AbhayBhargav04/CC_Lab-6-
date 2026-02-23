pipeline {
    agent any

    environment {
        HOST = "abhay_capstone@localhost"
        BASE_DIR = "/home/abhay_capstone/CC_LAB-6"
    }

    stages {

        stage('Build Backend Image') {
            steps {
                sh """
                ssh -o StrictHostKeyChecking=no \$HOST '
                    cd \$BASE_DIR/backend &&
                    docker build -t backend-app .
                '
                """
            }
        }

        stage('Run Backend Container') {
            steps {
                sh """
                ssh \$HOST '
                    docker rm -f backend || true
                    docker run -d --name backend --network app-network backend-app
                '
                """
            }
        }

        stage('Build NGINX Image') {
            steps {
                sh """
                ssh \$HOST '
                    cd \$BASE_DIR/nginx &&
                    docker build -t nginx-app .
                '
                """
            }
        }

        stage('Run NGINX Container') {
            steps {
                sh """
                ssh \$HOST '
                    docker rm -f nginx || true
                    docker run -d --name nginx --network app-network -p 8081:80 nginx-app
                '
                """
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
