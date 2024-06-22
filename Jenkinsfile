pipeline {
    agent any

    stages {
        stage('Build Image') {
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHub', url: 'https://github.com/VinmayParkhi/KNX-Test.git']])
                sh 'docker build -t ml-microservices .'
                echo 'Docker Image Build Successfully'
            }
        }
        stage('Publish Image') {
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"dockerPass",usernameVariable:"dockerUser")]){
                sh "docker login -u ${env.dockerUser} -p ${env.dockerPass}"
                sh "docker tag ml-microservices:latest ${env.dockerUser}/ml-microservices:latest"
                sh "docker push ${env.dockerUser}/ml-microservices:latest"
                echo 'Image Pushed to DockerHub'
                }
            }
        }
    }
}
