pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Faz o checkout do repositório do Git
                git 'https://github.com/rosangelalima/MobEAD.git'
            }
        }
        stage('Build') {
            steps {
                // Aqui seria o comando para compilar o seu código. 
                // Caso o projeto use Maven, o comando seria mvn clean install.
                sh 'mvn clean install' // ou outro comando de build dependendo do seu projeto.
            }
        }
        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('SONAR_TOKEN') // Referência ao token do SonarQube armazenado no Jenkins
            }
            steps {
                script {
                    def scannerHome = tool 'SonarQube Scanner'  // Nome da ferramenta SonarQube configurada no Jenkins
                    withSonarQubeEnv('SonarQube') {  // Nome do servidor SonarQube configurado no Jenkins
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=MobEAD -Dsonar.sources=. -Dsonar.login=${SONAR_TOKEN}"
                    }
                }
            }
        }
        stage('Quality Gate') {
            steps {
                waitForQualityGate abortPipeline: true // Verifica se a análise de qualidade passou
            }
        }
    }
}
