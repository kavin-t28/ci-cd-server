pipeline {
    agent any
    environment {
        COMPOSE_FILE = 'docker-compose.yml'
    }
    stages {
        stage('Docker Login') {
            steps {
                script {
                    // Docker login step to authenticate with Docker Hub
                    bat 'docker login -u kavint28 -p dckr_pat_PYe0TpNGkeBE9ecTJ7wVpUEmv4E'
                }
            }
        }
        stage('Clone Repositories') {
            steps {
                script {
                    bat 'git clone https://github.com/kavin-t28/microservice-1.git'
                    bat 'git clone https://github.com/kavin-t28/microservice-2.git'
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
