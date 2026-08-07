@Library('devops-shared-library') _

pipeline {

    agent {
        label 'docker-agent'
    }

    environment {
        IMAGE = 'YOUR_DOCKERHUB_USERNAME/rds-jenkins'
        TAG   = "${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                mavenBuild()
            }
        }

        stage('Docker Build') {
            steps {
                dockerBuild(
                    "${IMAGE}",
                    "${TAG}"
                )
            }
        }

        stage('Docker Push') {
            steps {
                dockerPush(
                    "${IMAGE}",
                    "${TAG}"
                )
            }
        }

        stage('Kubernetes Deploy') {
            steps {
                k8sDeploy(
                    'rds-jenkins',
                    'rds-jenkins',
                    "${IMAGE}:${TAG}",
                    'default'
                )
            }
        }
    }

    post {
        success {
            echo "Deployment successful: ${IMAGE}:${TAG}"
        }

        failure {
            echo "Pipeline failed."
        }
    }
}
