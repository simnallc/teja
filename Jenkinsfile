pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '5', daysToKeepStr: '5'))
        timestamps()
    }

    environment {
        registryCredential = credentials('docker')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    sh "docker build -t tejaswinivds24/image:latest ."
                }
            }
        }
        stage('Login to Docker Hub') {
            steps {
                script {
                    sh "echo $registryCredential_PSW | docker login -u $registryCredential_USR --password-stdin"
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    sh "docker push tejaswinivds24/image:latest"
                }
            }
        }
    }
}
