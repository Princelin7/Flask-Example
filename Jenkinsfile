pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:Princelin7/jenkins.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-example .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh '''
                if [ $(docker ps -a -q -f name=flask) ]; then
                    docker stop flask
                    docker rm flask
                fi
                docker run -d -p 5000:5000 --name flask flask-example
                '''
            }
        }
    }
}
