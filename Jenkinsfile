pipeline {  
    environment {
        sonarProjectKey = "MobEAD"  // Nome do seu projeto no SonarQube
        sonarHostURL = "http://localhost:9000"  // URL do SonarQube, ajuste conforme necessário
        sonarToken = "seu-token-sonarqube"  // Substitua pelo seu token do SonarQube
    }
    agent any 
    stages { 
        stage('Checkout from Git') {
            steps {
                // Faz o checkout do código do repositório Git
                git url: 'https://github.com/rosangelalima/MobEAD.git', branch: 'main' // Ajuste a URL e o branch conforme necessário
            }
        }
        stage('SonarQube Analysis') {
            steps {
                // Execute a análise do SonarQube
                withSonarQubeEnv('SonarQube') { // 'SonarQube' é o nome da instalação configurada no Jenkins
                    sh "sonar-scanner -Dsonar.projectKey=${sonarProjectKey} -Dsonar.sources=." // Ajuste o path conforme necessário
                }
            }
        }
    }
}
