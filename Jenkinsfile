node("docker") {
    sh "git rev-parse HEAD > .git/commit-id"
    def commit_id = readFile('.git/commit-id').trim()
    println commit_id

    stage "build"
    def app = docker.build "testimage"
}
