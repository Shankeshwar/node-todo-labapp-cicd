pipeline {
    agent { label 'Dev-Agent'}

    stages {
        stage('Checkout') {
            steps {
                git url:'https://github.com/Shankeshwar/node-todo-labapp-cicd.git', branch: 'main'
            }
        }
        stage('Build & Test') {
            steps {
                sh 'docker build . -t shankesh/node-todo-labapp-cicd:latest'
            }
        }
        stage('Login & Docker Push Image') {
            steps {
                echo 'Logging into DockerHub and push the docker image..'
                withCredentials([usernamePassword(credentialsId:'DockerHub',passwordVariable:'DockerHubPassword', usernameVariable:'DockerHubUsername')]) {
                    sh "docker login -u ${env.DockerHubUsername} -p ${env.DockerHubPassword}"
                    sh "docker push shankesh/node-todo-labapp-cicd:latest"
                }
            }
        }
        stage('Deploy'){
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
