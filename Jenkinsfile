podTemplate(label: 'docker-build', cloud: 'default',  containers: [
  containerTemplate(name: 'docker', image: 'docker:dind', ttyEnabled: true, command: 'cat', privileged: true, instanceCap: 1)
]) {
  stage('Build') {
    node('docker-build') {
      echo 'Building..'
      checkout scm
      sh './test_script.sh'
    }
  }
  stage('Test') {
    echo 'Testing..'
  }
  stage('Deploy') {
    echo 'Deploying....'
  }
}
