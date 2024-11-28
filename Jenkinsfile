pipeline{
  agent any
  environment {
  PATH = "/opt/maven/bin:$PATH"
  JAVA_HOME = "/usr/lib/jvm/java-1.17.0-openjdk-amd64"
  }
  stages{
    stage('Build'){
      steps{
        sh "mvn clean install"
        }
        }
    stage('SonarQube analysis'){
      steps{
        withSonarQubeEnv('sonarqube'){
          sh "mvn sonar:sonar"
          }
          }
          }
          }        
          }
      