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
        stage('SCM checkout') {
            steps {
                    git 'https://github.com/simnallc/teja.git'
                
            }
        }

        stage('Building image') {
            steps {
                    sh "docker build -t tejaswinivds24/app:$BUILD_NUMBER ."
                    sh "echo $registryCredential_PSW | docker login -u $registryCredential_USR --password-stdin"
            }
        }

        stage('Push Image') {
            steps {
                    sh "docker push tejaswinivds24/app:$BUILD_NUMBER"
            }
        }
    }
}
