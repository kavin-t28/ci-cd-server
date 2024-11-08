pipeline {
    agent any
    environment {
        COMPOSE_FILE = 'docker-compose.yml'
    }
    stages {
        stage('Clone Repositories') {
            steps {
                script {
                    // Clone each microservice repository
                    bat 'git clone https://github.com/kavin-t28/microservice-1.git'
                    bat 'git clone https://github.com/kavin-t28/microservice-2.git'
                }
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    bat 'docker build -t service1-image .\\service1-repo'
                    bat 'docker build -t service2-image .\\service2-repo'
                }
            }
        }
        stage('Start Services with Docker Compose') {
            steps {
                script {
                    bat "docker-compose -f ${COMPOSE_FILE} up -d"
                }
            }
        }
        stage('Run Integration Tests') {
            steps {
                script {
                    // Example integration test commands for each service
                    bat "curl -f http://localhost:3000"
                    bat "curl -f http://localhost:3001"
                }
            }
        }
    }
    post {
        always {
            script {
                bat "docker-compose -f ${COMPOSE_FILE} down"
            }
        }
    }
}
