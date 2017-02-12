podTemplate(label: 'docker-build',  containers: [
  containerTemplate(name: 'docker', image: 'docker:1.11-dind', ttyEnabled: true, command: 'cat')
],
volumes: [
  hostPathVolume(mountPath: "/var/run/docker.sock", hostPath: "/var/run/docker.sock")
]) {
  node('docker-build') {
    stage('Checkout') {
      checkout scm
    }
    stage('Build') {
      echo 'Building..'
      container('docker') {
        echo 'In container'
        sh 'ls -al'
        sh 'pwd'
        sh 'docker build -t maoilir/test .'
        sh 'docker inspect -f {{.Id}} maoilir/test'
        docker.build('maoilir/test:0.0.1', '.')
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
