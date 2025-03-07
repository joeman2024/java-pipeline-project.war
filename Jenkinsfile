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
        
                deploy adapters: [tomcat9(credentialsId: 'TomcatKey', path: '', url: 'http://3.133.149.121:8080/manager/html')], contextPath: null, war: '**/*.war'
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
