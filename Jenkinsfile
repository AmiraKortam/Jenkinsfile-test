pipeline {
    agent any
    environment {
        WORKSPACE = "/var/jenkins_home/workspace/docker-hub"
        IMAGE_NAME = "amiramohammed/test-jenkins"
        IMAGE_TAG = "latest"
        DOCKER_HUB_CREDENTIALS = "docker-hub-credentials"
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    echo "Checking workspace directory..."
                    sh 'pwd'
                    sh 'ls -l'
                    sh 'git rev-parse --is-inside-work-tree || echo "Not a git repository!"'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    echo "Building Docker image..."
                    def myImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}", ".")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    echo "Pushing Docker image to Docker Hub..."
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_HUB_CREDENTIALS) {
                        docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()
                    }
                }
            }
        }
    }
}
