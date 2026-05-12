pipeline {
    agent any

    environment {
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

        stage('Check Docker Images') {
            steps {
                bat 'docker images'
            }
        }
    }
}
