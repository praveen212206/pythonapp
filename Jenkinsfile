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
        stage('Push Image') {
            steps {
                withDockerRegistry([ credentialsId: 'dockerHub', url: '' ]) {
                    script {
                        docker.image("${IMAGE_NAME}:${BUILD_TAG}").push("${BUILD_TAG}")
                        docker.image("${IMAGE_NAME}:${BUILD_TAG}").push('latest')
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh "docker run -d -p 3333:3333 ${IMAGE_NAME}:${BUILD_TAG}"
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
