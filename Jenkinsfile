pipeline {
    agent any

    environment {
        REPOSITORY = "${params.REPOSITORY}"
        BRANCH = "${params.BRANCH}"
        BUCKET = "${params.BUCKET}"
        ROLE_ARN = credentials('ROLE_ARN')
        ACCOUNT = credentials('ACCOUNT')
    }

    stages {
        stage('Clone Repository') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: "refs/heads/${BRANCH}"]],
                    userRemoteConfigs: [[url: "${REPOSITORY}"]]
                ])
            }
        }

        stage('Copying to S3') {
            steps {
                withAWS(role: "${ROLE_ARN}", roleAccount: "${ACCOUNT}") {
                  sh "aws s3 sync . s3://${BUCKET}"
                }
            }
        }
    }
}
