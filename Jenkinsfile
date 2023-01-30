pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage ('Deploy_staging'){
            when {
            branch 'master'
            }
            steps{
                 sshPublisher(publishers: [sshPublisherDesc(configName: 'Staging', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo /usr/bin/systemctl stop train-schedule && rm -rf /opt/train-schedule/* && unzip -d /opt/train-schedule && sudo /usr/bin/systemctl start train-schedule', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/', remoteDirectorySDF: false, removePrefix: 'dist', sourceFiles: 'dist/train-schedule')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
