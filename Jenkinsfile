pipeline {
    agent any

    environment {
        IMAGE_NAME = "node-todo-app"
        CONTAINER_NAME = "node-todo-container"
        TAG = "latest"
    }

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/hmishra87/awswebsite-node-todo-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker rm -f $CONTAINER_NAME || true'
            }
        }

        stage('Remove Old Image') {
            steps {
                sh 'docker rmi $IMAGE_NAME:$TAG || true'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$TAG .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3001:3000 --name $CONTAINER_NAME $IMAGE_NAME:$TAG'
            }
        }
    }
}
