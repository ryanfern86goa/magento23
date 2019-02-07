pipeline {
    agent any
    // Clean workspace before doing anything

    stages {
        stage ('Clone') {
            when{
              branch 'master'
            }
            steps {
                deleteDir()
                checkout scm
            }
        }
        stage ('Build') {
            when{
              branch 'master'
            }
            steps {
                sh "echo 'master shell scripts to build project...'"
            }
        }
        stage ('Tests') {
            when{
              branch 'master'
            }
            steps {
                parallel 'static': {
                sh "echo 'shell scripts to run static tests...'"
                },
                'unit': {
                    sh "echo 'shell scripts to run unit tests...'"
                },
                'integration': {
                    sh "echo 'shell scripts to run integration tests...'"
                }
            }
            
        }
        stage ('Deploy') {
            when{
              branch 'master'
            }
            steps {
                sh "echo 'master shell scripts to deploy to server...'"
            }
        }
    }

}