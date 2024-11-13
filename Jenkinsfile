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
                    branches: [[name: "refs/tags/${BRANCH}"]], 
                    userRemoteConfigs: [[url: 'https://github.com/brambillagabrielle/repositorio-teste.git']]
                ])
            }
        }
    }
}
