pipeline {
    agent any
    // Clean workspace before doing anything
    deleteDir()

    stage ('Clone') {
        when{
          branch 'master'
        }
        steps {
            checkout scm
        }
    }
    stage ('Build') {
        when{
          branch 'master'
        }
        sh "echo 'master shell scripts to build project...'"
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

pipeline { 
    agent any
    // Clean workspace before doing anything
    deleteDir()

    stage ('Clone') {
        when{
          branch 'develop'
        }
        steps {
            checkout scm
        }
    }
    stage ('Build') {
        when{
          branch 'develop'
        }
        sh "echo 'develop shell scripts to build project...'"
    }
    stage ('Tests') {
        when{
          branch 'develop'
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
          branch 'develop'
        }
        steps {
            sh "echo 'develop shell scripts to deploy to server...'"
        }
    }
}
