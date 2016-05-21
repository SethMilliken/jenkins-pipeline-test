node('centos6') {
  wrap([$class: 'AnsiColorBuildWrapper', colorMapName: 'xterm']) {
    stage "Checkout"
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'WipeWorkspace'], [$class: 'UserExclusion', excludedUsers: '''uadeploy
eng-ops''']], submoduleCfg: [], userRemoteConfigs: [[url: 'git@github.com:urbanairship/pass-be.git']]])

    stage "Build"
    def MAV = tool name: 'ua maven', type: 'hudson.tasks.Maven$MavenInstallation'
    sh "${MAV}/bin/mvn clean"

    stage "Notify"
    slackSend channel: '#test-seth', color: 'good', message: "Job '${env.BUILD_TAG}' built on '${env.NODE_NAME}'"

  }


stage "promote"
input message: 'Promote Build', ok: 'Promote to Prod', parameters: [[$class: 'PromotedBuildParameterDefinition', description: '', jobName: "'${env.PROMOTED_JOB_NAME}'", name: "'${env.PROMOTED_NUMBER}'", process: '']]


}

