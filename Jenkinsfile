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
                deploy adapters: [tomcat9(credentialsId: 'tomcat-key', path: '', url: 'http://3.131.37.100:8080/')], contextPath: null, war: 'target/*.war'
            }
        }
    }
}
