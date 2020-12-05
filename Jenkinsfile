pipeline {
    agent any
    
    stages {
        stage('compile') {
            steps {
                sh 'mvn clean compile -e'    
            }
        }
        stage('test'){
            steps {
                sh 'mvn clean test -e'
            }
        }
        stage('jar'){
            steps {
                sh 'mvn clean package -e'
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv(installationName: 'sonar') {
                    sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                }
            }
        } 
        stage('run'){
            steps {
                sh 'nohup bash ./mvnw spring-boot:run &'
            }
        }
        stage('Curl') {
            steps {
                sh 'sleep 20'
                sh 'curl -X GET http://localhost:8081/rest/mscovid/test?msg=testing &'
            }
	    }
    }
}