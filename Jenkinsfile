pipeline {
    environment {
    registry = "tamasjit/AngularProject1"
    registryCredential = "dockerhub"
    dockerImage = ''
    PATH = "$PATH:/usr/local/bin"
}

    agent {
        'docker'}
    stages {
            stage('Cloning our Git') {
                steps {
                git 'https://github.com/tamasjit/hello-world-anguler.git'
                }
            }

            stage('Building Docker Image') {
                steps {
                    script {
                        dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
                }
            }

            stage('Deploying Docker Image to Dockerhub') {
                steps {
                    script {
                        docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                        }
                    }
                }
            }

            stage('Cleaning Up') {
                steps{
                  sh "docker rmi $registry:$BUILD_NUMBER"
                }
            }
        }
    }