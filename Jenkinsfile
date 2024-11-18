pipeline {
    agent any

    environment {
        BUCKET = "${params.BUCKET}"
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
                sh "aws s3 sync . s3://${BUCKET}"
            }
        }
    }
}
