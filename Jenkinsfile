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
                    app = docker.build("${IMAGE_NAME}:${BUILD_TAG}")
                }
            }
        }
        stage('Push Image') {
            steps {
                withDockerRegistry([ credentialsId: 'dockerHub', url: '' ]) {
                    script {
                        app.push("${BUILD_TAG}")
                        app.push('latest')
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh "docker run -itd -p 3333:3333 ${IMAGE_NAME}:${BUILD_TAG}"
                }
            }
        }
        stage('Remove Old Images') {
            steps {
                script {
                    sh "docker rmi ${IMAGE_NAME}:latest -f"
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
