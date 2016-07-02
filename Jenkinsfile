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

  def buildStage = { String id ->
    stage id
    sh "./b build -a dist --settings ${mvnSettingsFile} ${id}"
  }

  buildStage('poms')
  buildStage('jars')
  buildStage('strategoxt')
  buildStage('java')
  buildStage('java-uber')
  buildStage('language-prereqs')
  buildStage('languages')
  buildStage('dynsem')
  buildStage('spt')
  buildStage('eclipse-prereqs')
  buildStage('eclipse')
  buildStage('intellij-prereqs')
  buildStage('intellij')

  stage 'archive'
  archive 'dist/**/*'
}
