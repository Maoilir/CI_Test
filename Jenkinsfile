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

        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()

        def tag = "quay.io/maoilir/cidemo:${commit_id}"

        sh "docker build -t ${tag} ."
        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'Quay.io',
          usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
          sh "docker login -u $USERNAME -p $PASSWORD quay.io/maoilir"
          sh "docker push ${tag}"
        }
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
