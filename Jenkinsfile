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
        stage('sonar') {
            steps {
                withSonarQubeEnv(installationName: 'sonar') {
                    bat 'mvnw org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                }
            }
        }
        stage('uploadNexus'){
            steps {
                nexusPublisher nexusInstanceId: 'NexusJose',
                nexusRepositoryId: 'test-nexus',
                packages: [
                    [
                        $class: 'MavenPackage',
                        mavenAssetList: [
                            [
                                classifier: '',
                                extension: 'jar',
                                filePath: 'C:\\proyects\\diplomado\\maven\\ejemplo-maven\\build\\DevOpsUsach2020-0.0.1.jar'
                            ]
                        ],
                        mavenCoordinate: [
                            artifactId: 'spring-boot-starter-parent',
                            groupId: 'org.springframework.boot',
                            packaging: 'jar',
                            version: '0.0.1'
                        ]
                    ]
                ]
            }
        }
    }
}