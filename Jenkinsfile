@Library('jenkins-shared-library') _

pipeline {

agent {
    label 'docker-agent'
}

environment {
    IMAGE = 'ssankureddy392/rds-jenkins'
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

}
