pipeline {
    agent any

    environment {
        TAG = "${params.TAG}"
        REPOSITORY_URL = "${params.REPOSITORY_URL}"
        BUCKET_NAME = "${params.BUCKET_NAME}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: "refs/tags/${TAG}"]],
                    userRemoteConfigs: [[url: "${REPOSITORY_URL}"]]
                ])
            }
        }

        stage('Copy to S3') {
            steps {
                sh '''
                    aws s3 sync . s3://${BUCKET_NAME} \
                    --exclude ".git/*" \
                    --exclude "Jenkinsfile"
                '''
            }
        }
    }
}
