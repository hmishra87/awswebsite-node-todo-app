pipeline {
    agent any

    environment {
        IMAGE_NAME = "node-todo-app"
        CONTAINER_NAME = "node-todo-container"
        TAG = "latest"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/hmishra87/awswebsite-node-todo-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop $CONTAINER_NAME || true'
                sh 'docker rm $CONTAINER_NAME || true'
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
                sh 'docker run -d -p 8000:8000 --name $CONTAINER_NAME $IMAGE_NAME:$TAG'
            }
        }

        stage('Verify Container') {
            steps {
                sh 'docker ps | grep $CONTAINER_NAME'
            }
        }
    }
}
