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

  stage 'test'
  echo 'hello world'
}
