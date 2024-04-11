pipeline {
    agent any
    
    tools {
        maven "maven3.9.6"
    }

    stages {
        stage("Git clone") {
            steps {
                git 'https://github.com/kessiey/maven-build-website.git'
            }
        }

        stage("Build with Maven") {
            steps {
                sh "mvn clean"
            }
        }

        stage("Testing with Maven") {
            steps {
                sh "mvn test"
            }
        }

        stage("Package with Maven") {
            steps {
                sh "mvn package"
            }
        }

        stage('SonarQube Analysis') {
            environment {
                ScannerHome = tool 'sonar5.0'
            }
            steps {
                script {
                    withSonarQubeEnv('sonarqube') {
                        sh "${ScannerHome}/bin/sonar-scanner -Dsonar.projectKey=maven-build-website"
                    }
                }
            }
        }
    }
}