@Library('devops-shared-library') _

pipeline {

```
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

    stage('Docker Deploy') {
        steps {
            dockerDeploy(
                "${IMAGE}",
                "${TAG}"
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
```

}
