pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }

    environment {
        registry = "tejaswinivds24/app"
        registryCredential = credentials('docker')
        imageName = "${registry}:${BUILD_NUMBER}"
    }

    stages {
        stage('Building image') {
            steps {
                script {
                    echo "Building Docker image: ${imageName}"
                    dockerImage = docker.build(imageName)
                }
            }
        }

        stage('Deploy Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        
        stage('Check Image Status') {
            steps {
                script {
                    def imageInfo = dockerImage.inspector().getImageInfo()
                    echo "Image ID: ${imageInfo.getId()}"
                    echo "Image Name: ${imageInfo.getRepoTags()}"
                    // You can access more metadata about the image using other methods of imageInfo
                }
            }
        }
    }
}
