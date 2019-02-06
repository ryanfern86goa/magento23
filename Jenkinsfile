node {
    // Clean workspace before doing anything
    deleteDir()

    try {
        stage ('Clone') {
            checkout scm
        }
        stage ('Build') {
            sh "echo 'shell scripts to build project...'"
            archiveArtifacts artifacts: '*'
            copyArtifacts(projectName: "${JOB_NAME}", selector: specific("${built.number}"), target: "/home/ubuntu);
            sshPublisher(publishers: [sshPublisherDesc(configName: 'ec2-jenkins', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/home/ubuntu', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '/')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
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
