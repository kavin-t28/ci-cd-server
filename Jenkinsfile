pipeline {
    agent any
    environment {
        COMPOSE_FILE = 'docker-compose.yml'
    }
    stages {
        stage('Clone Repositories') {
            steps {
                script {
                    // Check if the directory exists, then clone
                    bat 'if not exist microservice-1 (git clone https://github.com/your-org/microservice-1.git)'
                    bat 'if not exist microservice-2 (git clone https://github.com/your-org/microservice-2.git)'
                }
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    bat 'docker build -t service1-image .\\microservice-1'
                    bat 'docker build -t service2-image .\\microservice-2'
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
