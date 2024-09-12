pipeline {
    agent any
    environment {
        NAME = "pythonapp"
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
    }
    stage ('Build Docker Image') {
            steps {
                sh "docker build -t $NAME ."
            }
    }
}
