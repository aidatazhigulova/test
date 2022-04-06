pipeline {
    agent { label "salve" }
    stages {
        stage('Clone repository') {
            steps {
                git 'https://github.com/aidatazhigulova/test.git'
            }
        }
        stage('Build image') {
            steps {
                echo 'Starting to build docker image'

                script {
                   docker.build("user/node-web-app")
                }
            }
        }
        stage('Push image'){
            steps{
                echo 'Pushing Docker Image'

                 script {
                    docker.withRegistry('nexus.sberbank.kz:5014') {
                        docker.image("user/node-web-app").push()
                        docker.image("user/node-web-app").push("latest")
                    }
                 }
            }
        }
    }
}