pipeline {
    agent any

    tools {
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                
                git branch: 'main', url: 'https://github.com/vytec-insurance1/core-app.git'

                sh "mvn -Dmaven.test.failure.ignore=true clean deploy"

            }

            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
