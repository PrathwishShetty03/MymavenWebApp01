pipeline {
    agent any

    tools {
        maven 'Maven'   // Use Maven (NOT Gradle)
        jdk 'JDK'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/PrathwishShetty03/MymavenWebApp01.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build SUCCESSFUL!'
        }
        failure {
            echo '❌ Build FAILED!'
        }
    }
}
