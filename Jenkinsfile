pipeline {
    agent any
    environment {
        COMPOSE_FILE = 'C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\ci-cd-pipeline\\docker-compose.yml'  // Full path to docker-compose.yml
    }
    stages {
        stage('Clean Workspace') {
            steps {
                script {
                    // Delete existing directories if they exist
                    bat 'if exist C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\ci-cd-pipeline\\microservice-1 rmdir /s /q C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\ci-cd-pipeline\\microservice-1'
                    bat 'if exist C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\ci-cd-pipeline\\microservice-2 rmdir /s /q C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\ci-cd-pipeline\\microservice-2'
                }
            }
        }
        stage('Clone Repositories') {
            steps {
                script {
                    // Clone repositories after cleaning workspace
                    bat 'git clone https://github.com/kavin-t28/ms1.git C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\ci-cd-pipeline\\microservice-1'
                    bat 'git clone https://github.com/kavin-t28/ms2.git C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\ci-cd-pipeline\\microservice-2'
                }
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    bat 'docker build -t service1-image C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\ci-cd-pipeline\\microservice-1'
                    bat 'docker build -t service2-image C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\ci-cd-pipeline\\microservice-2'
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
    }
    post {
        always {
            script {
                bat "docker-compose -f ${COMPOSE_FILE} down"
            }
        }
    }
}
