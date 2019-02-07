node ('master'){
    // Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
            when{
              branch 'master'
            }
            checkout scm
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
            parallel 'static': {
                sh "echo 'master shell scripts to run static tests...'"
            },
            'unit': {
                sh "echo 'master shell scripts to run unit tests...'"
            },
            'integration': {
                sh "echo 'master shell scripts to run integration tests...'"
            }
        }
        stage ('Deploy') {
            when{
              branch 'master'
            }
            sh "echo 'master shell scripts to deploy to server...'"
        }
    } catch (err) {
        currentBuild.result = 'master FAILED'
        throw err
    }
}

node ('master'){
    // Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
            when{
              branch 'develop'
            }
        stage ('Build') {
            when{
              branch 'develop'
            }
            sh "echo 'dev shell scripts to build project...'"
        }
        stage ('Tests') {
            when{
              branch 'develop'
            }
            parallel 'static': {
                sh "echo 'dev shell scripts to run static tests...'"
            },
            'unit': {
                sh "echo 'dev shell scripts to run unit tests...'"
            },
            'integration': {
                sh "echo 'dev shell scripts to run integration tests...'"
            }
        }
        stage ('Deploy') {
            when{
              branch 'develop'
            }
            sh "echo 'dev shell scripts to deploy to server...'"
        }
    } catch (err) {
        currentBuild.result = 'dev FAILED'
        throw err
    }
}