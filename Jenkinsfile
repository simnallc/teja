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
        echo "imageName: ${imageName}"
    }

    stages {
        stage('Building image') {
            steps {
                script {
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
    }
}
