pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = credentials('dockerhubJ') // Credentials ID for DockerHub
        DOCKER_IMAGE_NAME = 'bhavesh.gangurde@neosoftmail.com/myrepo' // Docker image name
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(env.DOCKER_IMAGE_NAME)
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', env.DOCKER_CREDENTIALS) {
                        docker.image(env.DOCKER_IMAGE_NAME).push()
                    }
                }
            }
        }
    }
}
