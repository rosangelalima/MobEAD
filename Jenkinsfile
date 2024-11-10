pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Faz o checkout do repositório
                git 'https://github.com/rosangelalima/MobEAD.git'  // Substitua pela URL do seu repositório
            }
        }
        stage('Build') {
            steps {
                // Adicione os comandos de build aqui, como Maven, Gradle, etc.
                sh 'mvn clean install'  // Exemplo para Maven, substitua conforme necessário
            }
        }
        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('SONAR_TOKEN')  // Referência ao token armazenado no Jenkins
            }
            steps {
                script {
                    def scannerHome = tool 'SonarQube Scanner'  // Nome da ferramenta configurada no Jenkins
                    withSonarQubeEnv('SonarQube') {  // Nome do servidor SonarQube configurado no Jenkins
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=MobEAD -Dsonar.sources=. -Dsonar.login=${SONAR_TOKEN}"
                    }
                }
            }
        }
        stage('Quality Gate') {
            steps {
                waitForQualityGate abortPipeline: true  // Aguarda pela análise de qualidade do SonarQube
            }
        }
    }
}
