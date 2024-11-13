pipeline {
    agent any

    environment {
        BRANCH = "${params.BRANCH}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: "refs/heads/${BRANCH}"]], 
                    userRemoteConfigs: [[url: 'https://github.com/brambillagabrielle/repositorio-teste.git']]
                ])
            }
        }

        stage('Copying to S3') {
            steps {
                sh "aws s3 sync . s3://devstore-teste-pipeline-jenkins/"
            }
        }
    }
}
