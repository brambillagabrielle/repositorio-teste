pipeline {
    agent any

    environment {
        BRANCH = "${params.BRANCH}"
    }

    stages {
        stage('Show Parameters') {
            steps {
                // Exibe o valor do parâmetro BRANCH no console para validação
                sh 'echo "Branch ou tag selecionado: ${BRANCH}"'
            }
        }
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
