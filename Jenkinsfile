pipeline {
    agent any
    // Clean workspace before doing anything

    stages {
        stage ('Clone master') {
            when{
              branch 'master'
            }
            steps {
                deleteDir()
                checkout scm
            }
        }
        
        stage ('Clone develop') {
            when{
              branch 'develop'
            }
            steps {
                deleteDir()
                checkout scm
            }
        }
        
        stage ('Build master') {
            when{
              branch 'master'
            }
            steps {
                sh "echo 'master shell scripts to build project...'"
            }
        }
        
        stage ('Build develop') {
            when{
              branch 'develop'
            }
            steps {
                sh "echo 'develop shell scripts to build project...'"
                sh "echo 'running artifact build'"
                zip zipFile: 'artifact.zip', archive: false, dir: './'
                sh "echo 'archiving artifact'"
                archiveArtifacts artifacts: 'artifact.zip'
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
