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
  sh './b gen-mvn-settings -SUyd settings.xml'

  stage 'poms'
  sh './b build --settings settings.xml poms'

  stage 'java'
  sh './b build --settings settings.xml java'

  stage 'strategoxt'
  sh './b build --settings settings.xml strategoxt'

  stage 'java'
  sh './b build --settings settings.xml java'
}
