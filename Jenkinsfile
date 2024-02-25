pipeline {
    agent any

    stages{
        stage('Checkout Source') {
            steps{
                git url: 'https://github.com/hubpagec/password_generate', branch: 'master'
            }
        }
        stage('Build Docker image') {
            steps{
                script{
                    dockerapp = docker.build("devops/passwod_generate:${env.BUILD}",
                        '-f ./Dokerfile .')
                }

            }
        }
        stage('Push Docker Image') {
            steps{
                script{
                    docker.withRegistry('http://192.168.3.138', 'harbor'){
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
    }
}