pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'sonarqube' // Nombre del servidor configurado en Jenkins
        SONARQUBE_TOKEN = credentials('sonarqube') // Credenciales de SonarQube
    }

    stages {
        stage('Validar Conexión con SonarQube') {
            steps {
                script {
                    echo "Validando conexión con SonarQube..."
                    def status = sh(script: "curl -s -o /dev/null -w '%{http_code}' http://sonarqube:9000", returnStdout: true).trim()
                    if (status != '200') {
                        error "SonarQube no está disponible en http://sonarqube:9000. Código de estado: ${status}"
                    }
                }
            }
        }
        stage('Análisis de Código con SonarQube') {
            steps {
                withSonarQubeEnv('sonarqube') { // Utiliza el nombre configurado en "SonarQube Servers"
                    script {
                        def scannerHome = tool 'sonarqube' // Nombre del scanner configurado
                        sh """
                            ${scannerHome}/bin/sonar-scanner \
                            -Dsonar.projectKey=jenkins \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://sonarqube:9000 \
                            -Dsonar.login=${SONARQUBE_TOKEN}
                        """
                    }
                }
            }
        }
    }
}
     
