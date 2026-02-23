pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Validate Backend Directory') {
            steps {
                sh 'ls backend'
            }
        }

        stage('Validate NGINX Directory') {
            steps {
                sh 'ls nginx'
            }
        }
    }

    post {
        success {
            echo 'Task 4 Pipeline executed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
