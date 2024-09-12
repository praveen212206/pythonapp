pipeline {
    agent any
    environment {
        APPLICATION = "pythonapp"
        DOCKERHUB_ACCOUNT_ID = "praveen2106"
        IMAGE_NAME = "${DOCKERHUB_ACCOUNT_ID}/${APPLICATION}"
        BUILD_TAG = "${BUILD_NUMBER}"
    }
    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }
        stage('Build Image') {
            steps {
                script {
                    def app = docker.build("${IMAGE_NAME}:${BUILD_TAG}")
                }
            }
        }
}
