pipeline {
    agent any
    environment {
        COMPOSE_FILE = 'docker-compose.yml'
    }
    stages {
        stage('Clone Repositories') {
            steps {
                script {
                    // Adjust the paths for where the repositories are located
                    bat 'git clone https://github.com/your-org/microservice-1.git'
                    bat 'git clone https://github.com/your-org/microservice-2.git'
                }
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    // Adjust paths to match the cloned directories under Jenkins workspace
                    bat 'docker build -t service1-image .\\microservice1'
                    bat 'docker build -t service2-image .\\microservice2'
                }
            }
        }
        stage('Start Services with Docker Compose') {
            steps {
                script {
                    // Make sure the docker-compose.yml is in the correct location
                    bat "docker-compose -f ${COMPOSE_FILE} up -d"
                }
            }
        }
        stage('Run Integration Tests') {
            steps {
                script {
                    // Ensure your services are available on these ports
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
