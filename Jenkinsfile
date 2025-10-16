Place Jenkinsfile in your repo:
pipeline {
 agent any
 environment {
 DOCKER_IMAGE = "siddhimokashi/my-web" //provide docker username
 }
 stages {
 stage('Checkout') {
 steps {
 git 'https://github.com/siddhi10101/exp8.git' //provide GitHub repo URL
 }
 }
 stage('Build Docker Image') {
 steps {
 script {
 sh 'docker build -t $DOCKER_IMAGE .'
 }
 }
 }
 stage('Push to DockerHub') {
 steps {
 withCredentials([usernamePassword(credentialsId: 'dockerhub-cred',
usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
 sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --passwordstdin"
 sh "docker push $DOCKER_IMAGE"
 }
 }
 }
 stage('Deploy Container') {
 steps {
 sh "docker run -d -p 8080:80 --name my-web-app-container $DOCKER_IMAGE"
 }
 }
 }
}