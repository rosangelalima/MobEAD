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
                // Adicione os comandos de build aqui, por exemplo, para um projeto Maven
                echo 'Executando build do projeto'  // Mensagem simples para debug
                // Exemplo para rodar Maven, descomente a linha abaixo se o projeto usar Maven:
                // sh 'mvn clean install'  // Se for Maven, descomente
            }
        }
        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('SONAR_TOKEN')  // Referência ao token armazenado no Jenkins
            }
            steps {
                script {
                    // Definindo o caminho do scanner do SonarQube
                    def scannerHome = tool 'SonarQube Scanner'  // Nome da ferramenta configurada no Jenkins
                    withSonarQubeEnv('SonarQube') {  // Nome do servidor SonarQube configurado no Jenkins
                        // Comando para executar o SonarQube Scanner
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=MobEAD -Dsonar.sources=. -Dsonar.login=${SONAR_TOKEN}"
                    }
                }
            }
        }
        stage('Quality Gate') {
            steps {
                // Verifica a análise de qualidade no SonarQube e, se não aprovado, aborta a pipeline
                waitForQualityGate abortPipeline: true  // Se o Quality Gate falhar, a pipeline será abortada
            }
        }
    }
}
