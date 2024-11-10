pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'  // URL do SonarQube
        SONAR_TOKEN = credentials('sonar-token')  // Credenciais armazenadas no Jenkins
    }

    tools {
        // Definir a instalação do SonarQube Scanner configurado no Jenkins
        sonarQubeScanner 'SonarQubeScanner' // Nome configurado na seção de ferramentas do Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Clonar o código do repositório Git
                git url: 'https://github.com/seu-usuario/seu-repositorio.git', branch: 'main'
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
                // Realizar o build do código
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                // Realizar o deploy (caso tenha essa etapa no seu processo)
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
