pipeline {
    agent any
    
    environment {
        SONAR_VERSION = '10.4' // Change this to your SonarQube version
        SONAR_HOST_URL = 'http://localhost:9000' // Change this to your SonarQube server URL
        SONAR_TOKEN = credentials('jenkins') // Use Jenkins credentials for your SonarQube token
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your code from version control
                git 'https://github.com/jawadsaeed26/git-demo.git'
            }
        }
        
        stage('Build') {
            steps {
                // Build your project (compilation)
                sh 'javac HelloWorld.java'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                script {
                    // Download and configure SonarScanner
                    def scannerHome = tool 'sonar-scanner'
                    withEnv(["PATH+SONARSCANNER=${scannerHome}/bin"]) {
                        // Run SonarScanner
                        sh 'sonar-scanner \
                            -Dsonar.projectKey=my_project_key \
                            -Dsonar.sources=. \
                            -Dsonar.java.binaries=. \
                            -Dsonar.host.url=${SONAR_HOST_URL} \
                            -Dsonar.login=${SONAR_TOKEN}'
                    }
                }
            }
        }
    }
}
