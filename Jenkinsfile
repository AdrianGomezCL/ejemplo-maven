pipeline {
    agent any
    
    stages {
        stage('compile') {
            steps {
                bat './mvnw.cmd clean compile -e'
            }
        }
        stage('test'){
            steps {
                bat './mvnw.cmd clean test -e'
            }
        }
        stage('jar'){
            steps {
                bat './mvnw.cmd clean package -e'
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv(installationName: 'sonar') {
                    bat 'mvnw org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                }
            }
        } 
        stage('run'){
            steps {
                sleep 20
                bat 'start mvnw.cmd spring-boot:run'
            }
        }
        stage('Curl') {
            steps {
                sleep 20
                bat 'curl -X GET "http://localhost:8081/rest/mscovid/test?msg=testing"'
            }
	    }
    }
}