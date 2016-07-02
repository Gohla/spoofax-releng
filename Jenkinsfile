properties [[$class: 'BuildDiscarderProperty', strategy: [$class: 'LogRotator', artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '3']]]
node {
  stage 'checkout'
  checkout([
    $class: 'GitSCM',
    branches: [[name: env.BRANCH_NAME]],
    extensions: [
      [$class: 'CloneOption', timeout: 60],
      [$class: 'CheckoutOption', timeout: 60],
      [$class: 'SubmoduleOption', recursiveSubmodules: true, trackingSubmodules: true, timeout: 60],
      [$class: 'CleanCheckout'],
      [$class: 'CleanBeforeCheckout']
    ],
    userRemoteConfigs: [[refspec: "+refs/heads/${env.BRANCH_NAME}:refs/remotes/origin/${env.BRANCH_NAME}", url: 'https://github.com/Gohla/spoofax-releng.git']]
  ])

  stage 'gen mvn settings'
  def mvnSettingsFile = "${pwd()}/settings.xml"
  sh "./b gen-mvn-settings -Uyd ${mvnSettingsFile}"

  stage 'poms'
  sh "./b build --settings ${mvnSettingsFile} poms"

  stage 'jars'
  sh "./b build --settings ${mvnSettingsFile} jars"

  stage 'strategoxt'
  sh "./b build --settings ${mvnSettingsFile} strategoxt"

  stage 'java'
  sh "./b build --settings ${mvnSettingsFile} java"
}
