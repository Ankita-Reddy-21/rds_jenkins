```groovy
@Library('devops-shared-library') _

pipeline {

    agent {
        label 'docker-agent'
    }

    environment {
        IMAGE = 'your-dockerhub-username/myapp'
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
                    'myapp',
                    'myapp',
                    "${IMAGE}:${TAG}",
                    'default'
                )
            }
        }
    }
}
```

