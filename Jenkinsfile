pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh './gradlew clean build --no-daemon'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
        stage('Package') {
            steps {
                sh './gradlew bootJar'
            }
        }
    }
    post {
        always {
            junit {
                testResults: '**/build/test-results/test/*.xml'
            }
            recordIssues(
                enabledForFailure: true, aggregatingResults: true, 
                tools: [java(), checkStyle(pattern: '**/build/reports/checkstyle/main.xml', reportEncoding: 'UTF-8')]
            )
        }
        
    }
}
