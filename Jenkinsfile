pipeline {
    agent any

    environment {
        DOCKER_HUB_REPO = 'cihuahuahua/java-maven-app'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/LulukDWiKuncoro/praktikum-ci-cd.git'
            }
        }

        stage('Build with Maven') {
            steps {
                bat '''
                mvn clean package
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '''
                docker build -t %DOCKER_HUB_REPO%:1.0 .
                '''
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat '''
                    docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat '''
                docker tag %DOCKER_HUB_REPO%:1.0 %DOCKER_HUB_REPO%:1.0
                docker push %DOCKER_HUB_REPO%:1.0
                '''
            }
        }
    }
}
