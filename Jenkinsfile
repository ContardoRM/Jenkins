node("docker") {
    docker.withRegistry('contardo.acuna@gmail.com', 'docker-hub-credentials') {
    
        git url: "https://github.com/ContardoRM/HelloWorldCI", credentialsId: 'git-hub-credentials'
    
        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
        def app = docker.build "Test Jenkins"
    
        stage "publish"
        app.push 'master'
        app.push "${commit_id}"
    }
}
