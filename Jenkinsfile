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
                // Caso o projeto não precise de uma ferramenta como Maven ou Gradle, pode usar o 'echo'
                echo 'Executando build do projeto'  // Comando simples de exemplo
                // Exemplo para rodar Maven:
                // sh 'mvn clean install'  // Se o projeto usar Maven, descomente esta linha
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
                        // Executa o comando para rodar o SonarQube Scanner
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=MobEAD -Dsonar.sources=. -Dsonar.login=${SONAR_TOKEN}"
                    }
                }
            }
        }
        stage('Quality Gate') {
            steps {
                // Verifica a análise de qualidade no SonarQube e, se não aprovado, aborta a pipeline
                waitForQualityGate abortPipeline: true  // Se o Quality Gate falhar, o pipeline será abortado
            }
        }
    }
}
