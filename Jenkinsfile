pipeline {
    agent any
    
    environment {
        DOCKER_HUB_USERNAME = 'tejaswinivds24'
        DOCKER_HUB_PASSWORD = 'tejaswini24'
        DOCKER_IMAGE_NAME = 'firstimage'
        DOCKERFILE_PATH = '/home/ec2-user/Dockerfile' // Relative path to your Dockerfile
    }
    echo "line 10"
    stages {
        echo "line 11"
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(env.DOCKER_IMAGE_NAME, "-f ${env.DOCKERFILE_PATH} .")
                }
            }
        }
        echo "line 20"
        stage('Push to Docker Hub') {
            steps {
                script {
                    echo "line 24"
                    docker.withRegistry('https://index.docker.io/v1/', env.DOCKER_HUB_USERNAME, env.DOCKER_HUB_PASSWORD) {
                        docker.image(env.DOCKER_IMAGE_NAME).push()
                    }
                }
            }
        }
    }
}

