pipeline {
    agent any

    stages {
        stage('build project') {
            steps {
                git url: 'https://github.com/NaveenkumarcumM/bankapp-eta-app.git', branch: "master"
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t naveencum98/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push naveencum98/staragileprojectfinance:v1'
            }
        }

        stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name My-first-container2211 -p 8083:80 naveencum98/staragileprojectfinance:v1'
            }
        }
    }
}
