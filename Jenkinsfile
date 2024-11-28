pipeline {
	agent any
	
	environment {
		SONARQUBE_ENV = 'SonarQube' // Configuraci´on registrada en Jenkins
	}
	stages {
		stage('Checkout') {
			steps {
			echo 'Clonando el repositorio...'
			checkout scm
		}
	}
	
	stage('Build') {
		steps {
			echo 'Compilando el proyecto...'
			sh 'mvn clean package'
		}
	}
	
	
	stage('SonarQube Analysis') {
		steps {
			echo 'Ejecutando an´alisis de SonarQube...'
			withSonarQubeEnv(SONARQUBE_ENV) {
				sh 'mvn sonar:sonar'
			}
			10
			Proyecto 2
		}
	}
	
	stage('Quality Gate') {
		steps {
			timeout(time: 5, unit: 'MINUTES') {
				waitForQualityGate abortPipeline: true
			}
		}
	}
}