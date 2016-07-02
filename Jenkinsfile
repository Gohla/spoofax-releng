stage 'checkout'
node {
  checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CloneOption', depth: 0, noTags: false, reference: '', shallow: false, timeout: 60], [$class: 'CheckoutOption', timeout: 60], [$class: 'SubmoduleOption', disableSubmodules: false, recursiveSubmodules: true, reference: '', trackingSubmodules: true], [$class: 'CleanCheckout'], [$class: 'CleanBeforeCheckout']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Gohla/spoofax-releng.git']]])
  sh './b'
  stage 'after checkout'
  echo 'inside node'
}

stage 'after node'
echo 'after node'
