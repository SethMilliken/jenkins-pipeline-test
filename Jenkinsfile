node('centos6') {
  //wrap(<object of type hudson.plugins.ansicolor.AnsiColorBuildWrapper>) {
    stage "Checkout"
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'WipeWorkspace'], [$class: 'UserExclusion', excludedUsers: '''uadeploy
eng-ops''']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/urbanairship/pass-be/']]])

    stage "Build"
    def MAV = tool name: 'ua maven', type: 'hudson.tasks.Maven$MavenInstallation'
    sh "${MAV}/bin/mvn clean"

    stage "Notify"
    slackSend channel: '#test-seth', color: 'good', message: 'slack test send'
  //}

}
