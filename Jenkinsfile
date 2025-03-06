pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Build success'
                    archiveArtifacts artifacts: '**/target/*.war', onlyIfSuccessful: true
                }
                failure {
                    echo 'Build failed'
                }
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                echo 'Deploying the project...'
                sh 'cp -r target/*.war /opt/apache-tomcat-9.0.100/webapps'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the project...'
                // Add your test steps here
            }
        }
    }
}
