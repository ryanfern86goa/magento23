node ('master'){
    // Clean workspace before doing anything
    deleteDir()

    try {
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
                parallel {
                    'static': {
                        sh "echo 'master shell scripts to run static tests...'"
                    },
                    'unit': {
                        sh "echo 'master shell scripts to run unit tests...'"
                    },
                    'integration': {
                        sh "echo 'master shell scripts to run integration tests...'"
                    }
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
                parallel {
                    'static': {
                        sh "echo 'develop shell scripts to run static tests...'"
                    },
                    'unit': {
                        sh "echo 'develop shell scripts to run unit tests...'"
                    },
                    'integration': {
                        sh "echo 'develop shell scripts to run integration tests...'"
                    }
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
    } catch (err) {
        currentBuild.result = 'develop FAILED'
        throw err
    }
}