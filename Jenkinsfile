node {
  git url: 'https://github.com/SethMilliken/jenkins-pipeline-test.git'
  stage "Stage 1"
  sh "echo hello, world"
  stage "Stage 2"
  slackSend channel: '#test-seth', color: 'good', message: 'slack test send'
}
