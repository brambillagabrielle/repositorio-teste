pipeline {
    agent any

    environment {
        TAG = "${params.TAG}"
        BUCKET = "${params.BUCKET}"
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
                sh "aws s3 sync . s3://${BUCKET}"
            }
        }
    }
}
