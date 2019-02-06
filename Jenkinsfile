node {
    // Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
            checkout scm
        }
        stage ('Build') {
            sh "echo 'shell scripts to build project...'"
            zip zipFile: 'artifact.zip', archive: false, dir: './'
            archiveArtifacts artifacts: 'artifact.zip'
            sshPublisher(publishers: [sshPublisherDesc(configName: 'ec2-jenkins', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'mkdir releases & cd releases  & mkdir ${BUILD_NUMBER} & cd ${BUILD_NUMBER} & unzip ../../artifact.zip', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/home/ubuntu', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'artifact.zip')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            sh "scp -o StrictHostKeyChecking=no $WORKSPACE/auth.json ubuntu@ec2-18-191-172-33.us-east-2.compute.amazonaws.com:/home/ubuntu/"
        }
        stage ('Tests') {
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
        stage ('Deploy') {
            sh "echo 'shell scripts to deploy to server...'"
        }
    } catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }
}
