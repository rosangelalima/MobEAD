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
                // Se o projeto não utilizar Maven ou Gradle, você pode rodar um comando simples como "echo"
                echo 'Executando build do projeto' // Exemplo de comando simples
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
                        // Comando que executa o scanner do SonarQube
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=MobEAD -Dsonar.sources=. -Dsonar.login=${SONAR_TOKEN}"
                    }
                }
            }
        }
        stage('Quality Gate') {
            steps {
                // Verifica se a qualidade do código está ok no SonarQube
                waitForQualityGate abortPipeline: true  // Abortará o pipeline se a qualidade não for atendida
            }
        }
    }
}
