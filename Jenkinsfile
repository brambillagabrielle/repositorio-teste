pipeline {
    agent any

    environment {
        BUCKET_NAME = "${params.BUCKET_NAME}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Copying to S3') {
            steps {
                sh "aws s3 sync . s3://${BUCKET_NAME}"
            }
        }
    }
}
