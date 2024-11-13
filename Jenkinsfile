pipeline {
    agent any

    environment {
        TAG = "${params.TAG}"
        BUCKET = "${params.BUCKET}"
        ROLE_ARN = credentials('ROLE_ARN')
        ACCOUNT = credentials('ACCOUNT')
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    checkout([
                        $class: 'GitSCM', 
                        branches: [[name: "refs/tags/${TAG}"]],
                        userRemoteConfigs: [[url: scm.userRemoteConfigs[0].url]]
                    ])
                }
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
