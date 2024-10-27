pipeline {
    agent any

    environment {
        DOCKER_IMAGE = ''
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Сборка Docker-образа
                    DOCKER_IMAGE = docker.build("flask-cicd-app")
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Запуск тестов внутри контейнера
                    DOCKER_IMAGE.inside {
                        sh 'pytest test_app.py'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Запуск контейнера с пробросом порта 5002
                    sh 'docker-compose down'
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}
