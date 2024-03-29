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
                    echo "imageName: ${imageName}"
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
