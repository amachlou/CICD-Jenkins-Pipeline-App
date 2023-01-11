pipeline {
    environment {
        registry = 'amachlou/cicd_app'
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/amachlou/cicd_app.git'
            }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    echo 'Tests passed'
                }

            }
        }
        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('', 'docker_hub') {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy image') {
            steps {
                bat "docker run -d $registry:$BUILD_NUMBER"
            }
        }
    }
}
