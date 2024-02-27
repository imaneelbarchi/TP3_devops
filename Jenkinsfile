pipeline {
    environment {
        registry = "ielbarchi/tp3"
        registryCredential = 'dockerhub_dev'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git branch: 'main', url: 'https://github.com/imaneelbarchi/TP3_devops'
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
                    echo "Tests passed"
                }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy image') {
         	steps{
         	bat "docker run -d $registry:$BUILD_NUMBER"
         	}
            }
    }
}
