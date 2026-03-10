pipeline {
    agent any
    stages {
        stage('Clone') {
            steps { checkout scm }
        }
        stage('Build') {
            steps {
                sh 'docker build -t devops-agent-app .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run devops-agent-app python -m pytest || true'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop app || true'
                sh 'docker rm app || true'
                sh 'docker run -d --name app -p 80:5000 devops-agent-app'
            }
        }
    }
    post {
        success { echo 'Deployment Successful!' }
        failure { echo 'Deployment Failed!' }
    }
}