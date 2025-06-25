pipeline {
    agent any

    stages {
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/ShenanVindinu/GitHub-Docker-and-Jenkins-CI-CD-Pipeline.git'
                }
            }
        }
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t shenanvin/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'testdockerhubpass', variable: 'test-docker-hub-pass')]) {
                    bat "docker login -u shenanvin -p %test-docker-hub-pass%"
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push shenanvin/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}