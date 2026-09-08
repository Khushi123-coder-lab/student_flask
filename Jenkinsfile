pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test Application') {
            steps {
                sh 'python -m py_compile app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t student-flask-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop student-app || true'
                sh 'docker rm student-app || true'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'docker run -d -p 5000:5000 --name student-app student-flask-app'
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo 'Application deployed successfully using Jenkins.'
        }

        failure {
            echo 'Application deployment failed.'
        }
    }
}
