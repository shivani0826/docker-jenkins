pipeline {
    agent any

    environment {
        IMAGE = "node-app-image"
        CONTAINER = "node-app-container"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/shivani0826/docker-jenkins.git'
            }
        }

        stage('Docker Build Image') {
            steps {
                sh 'docker build -t $IMAGE ./node-app'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                if [ $(docker ps -q --filter name=$CONTAINER) ]; then
                    docker stop $CONTAINER
                    docker rm $CONTAINER
                fi
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d --name $CONTAINER -p 3000:3000 $IMAGE'
            }
        }
    }
}

