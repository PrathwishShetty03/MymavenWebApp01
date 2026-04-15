pipeline {
    agent any

    tools {
        maven 'Maven'   // Must match Jenkins tool name
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/PrathwishShetty03/MymavenWebApp01.git'
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

        stage('Deploy WAR to Tomcat') {
            steps {
                sh '''
                echo "Stopping Tomcat..."
                /opt/tomcat/bin/shutdown.sh || true
                sleep 5

                echo "Removing old WAR..."
                rm -rf /opt/tomcat/webapps/MymavenWebApp01*

                echo "Copying new WAR..."
                cp target/MymavenWebApp01.war /opt/tomcat/webapps/

                echo "Starting Tomcat..."
                /opt/tomcat/bin/startup.sh
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
