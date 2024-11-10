pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/rosangelalima/MobEAD.git'  // Substitua pela URL do seu repositório
            }
        }
        stage('Build') {
            steps {
                // Se não usar Maven ou Gradle, pode usar um comando simples, como echo
                echo 'Realizando build'
            }
        }
        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('SONAR_TOKEN')  // Token que você criou no Jenkins
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
                waitForQualityGate abortPipeline: true  // Aguarda a análise de qualidade
            }
        }
    }
}
