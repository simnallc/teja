pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }

    environment {
        registry = "tejaswinivds24/app"
        registryCredential = credentials('docker')
    }

    stages {
        stage('Building image') {
            steps {
                script {
                    echo "Registry: ${registry}"
                    echo "build: ${BUILD_NUMBER}"
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
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
