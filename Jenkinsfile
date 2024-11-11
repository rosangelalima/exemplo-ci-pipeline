pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'  // URL do SonarQube
        SONAR_TOKEN = credentials('SONAR_TOKEN')  // Credenciais armazenadas no Jenkins
    }

    tools {
        // Defina o nome da instalação do SonarQube Scanner configurada nas ferramentas do Jenkins
        sonarQubeScanner 'SonarQubeScanner'  // Nome configurado no Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Clona o código do repositório Git
                git url: 'https://github.com/rosangelalima/exemplo-ci-pipeline.git', branch: 'main'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Executa a análise do SonarQube
                    sh 'mvn clean install sonar:sonar -Dsonar.host.url=${SONAR_HOST_URL} -Dsonar.login=${SONAR_TOKEN}'
                }
            }
        }

        stage('Build') {
            steps {
                // Realiza o build do código
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                // Realiza o deploy (caso tenha essa etapa no seu processo)
                echo 'Deploying application...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
