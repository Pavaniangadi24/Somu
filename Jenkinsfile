pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockerhub-token'
        IMAGE_NAME = 'pavani2405/new_docker_image'
    }

    stages {

        stage('Build Java Application') {
            steps {
                bat 'javac HelloWorld.java'
            }
        }

        stage('Run Java Program') {
            steps {
                bat 'java HelloWorld'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:latest .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                credentialsId: 'dockerhub-token',
                usernameVariable: 'USER',
                passwordVariable: 'PASS')]) {

                    bat '''
                    docker logout
                    echo %PASS%> token.txt
                    set /p TOKEN=<token.txt
                    docker login -u %USER% -p %TOKEN%
                    del token.txt
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %IMAGE_NAME%:latest'
            }
        }
    }
}
