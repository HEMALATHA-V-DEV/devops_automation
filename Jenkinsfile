pipeline {
    agent any
    environment {
        DOCKER_HUB_REPO = "your-dockerhub-username/my-springboot-app"
        DOCKER_CREDENTIALS_ID = "docker-hub-credentials"
    }
    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/your-username/my-springboot-app.git'
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REPO}:${BUILD_NUMBER}")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        docker.image("${DOCKER_HUB_REPO}:${BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }
}
