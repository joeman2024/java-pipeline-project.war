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
        stage('Deploy') {
            steps {
                echo 'Deploying the project...'
                sh 'cp **/target/*.war /var/lib/tomcat/webapps/'
            }
        }
    }
}
