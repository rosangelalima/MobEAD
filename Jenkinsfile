pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'  // URL do seu servidor SonarQube
        SONAR_TOKEN = credentials('SONAR_TOKEN')  // Credenciais armazenadas no Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Clona o código do repositório Git
                git url: 'https://github.com/rosangelalima/MobEAD.git', branch: 'main'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Substitui as variáveis manualmente se necessário
                    bat 'mvn clean install sonar:sonar -Dsonar.host.url="http://localhost:9000" -Dsonar.login="sqa_b3eee5cabfe19d0c70a1722f4a64394e63c25725"'
                }
            }
        }

        stage('Build') {
            steps {
                // Realiza o build do código
                bat 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                // Realiza o deploy (se aplicável)
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
