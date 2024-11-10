pipeline {
    agent any  // Definir um agente para rodar o pipeline (pode ser qualquer agente disponível)

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/rosagnelalima/exemplo-ci-pipeline.git'  // Altere para o seu repositório
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'  // Comando de build com Maven
            }
        }
        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('SONAR_TOKEN')  // Use um token de autenticação do SonarQube
            }
            steps {
                script {
                    def scannerHome = tool 'SonarQube Scanner'  // Caminho do scanner do SonarQube configurado no Jenkins
                    withSonarQubeEnv('SonarQube') {  // Nome do servidor SonarQube configurado no Jenkins
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=exemplo-ci-pipeline -Dsonar.sources=src -Dsonar.login=${SONAR_TOKEN}"
                    }
                }
            }
        }
        stage('Quality Gate') {
            steps {
                waitForQualityGate abortPipeline: true  // Esperar o resultado da análise de qualidade do SonarQube
            }
        }
    }
}
