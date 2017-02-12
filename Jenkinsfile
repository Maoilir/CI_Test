podTemplate(label: 'docker-build',  containers: [
  containerTemplate(name: 'docker', image: 'docker:dind', ttyEnabled: true, command: 'cat')
]) {
  node('docker-build') {
    stage('Build') {
      echo 'Building..'
      container('docker') {
        echo 'In container'
        sh './test_script.sh'
        sh 'docker build .'
      }
    }
    stage('Test') {
      echo 'Testing..'
    }
    stage('Deploy') {
      echo 'Deploying....'
    }
  }
}
