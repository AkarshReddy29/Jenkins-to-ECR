pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    triggers {
        githubPush()
    }
    stages {
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }

        stage('Build') { 
            steps { 
                script{
                 app = docker.build("jenkins-test")
                }
            }
        }
        stage('Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{
                        docker.withRegistry('630511314671.dkr.ecr.us-east-1.amazonaws.com/', 'ecr:us-east-1:jenkinsecr-test') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
    }
}