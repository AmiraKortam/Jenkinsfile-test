pipeline {
    agent any
    environment {
        WORKSPACE = "/var/jenkins_home/workspace/Jenkins-NTI"
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    sh 'pwd'
                    sh 'ls -l'
                    sh 'git rev-parse --is-inside-work-tree || echo "Not a git repository!"'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('image1', '.')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/repository/docker/amiramohammed/test-jenkins/general', 'docker-hub-credentials') {
                        docker.image('image1').push('latest')
                    }
                }
            }
        }
    }
}
