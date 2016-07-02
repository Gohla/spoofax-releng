stage 'checkout'
node {
  sh 'git submodule update --init --remote --recursive'
  stage 'after checkout'
  echo 'inside node'
}

stage 'after node'
echo 'after node'
