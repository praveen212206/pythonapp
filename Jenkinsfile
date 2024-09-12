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
    }
}
