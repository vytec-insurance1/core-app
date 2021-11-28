pipeline {
    agent { label 'maven-label' }
      environment {
        YourTag = 'main'
    }
    tools {
        maven "M3"
    }
    stages {
        stage('User Input') {


            steps {

                script {
                        CHOICES = ["main", "dev", "test"];    
                        env.YourTag = input  message: 'What are we deploying today?',ok : 'Deploy',id :'tag_id',
                                        parameters:[choice(choices: CHOICES, description: 'Select a tag for this build', name: 'TAG')]
                        }           
                echo "Deploying ${env.YourTag}. Have a nice day."
            }
        }
        stage('prepare') {
            steps {
                git branch: '${env.YourTag}', url: 'https://github.com/vytec-insurance1/core-app.git'
                echo 'branch used :: ${env.YourTag}'
                //checkout scm
            }
        }
        stage('build') {
            steps {
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
