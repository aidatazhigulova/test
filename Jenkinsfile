pipeline {
    agent { label "salve" }
    stages {
        stage('Clone repository') {
            steps {
                git 'https://github.com/aidatazhigulova/test.git'
//                 git([url: 'https://github.com/aidatazhigulova/test.git', branch: 'main'])

                checkout scm
            }
        }
        stage('Build image') {
            steps {
                echo 'Starting to build docker image'

                script {
                   docker.build("user/node-web-app")
                }
            }
        stage('Push image'){
            steps{
                echo 'Pushing Docker Image'

                 script {
                    docker.withRegistry('https://nexus.sberbank.kz:5014') {
                        docker.image("user/node-web-app").push()
                        docker.image("user/node-web-app").push("latest")
                    }
            }
        }
    }
}




