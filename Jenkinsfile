node("docker") {
      
        git url: "https://github.com/ContardoRM/Jenkins.git", credentialsId: 'git-hub-credentials'
    
        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
        def app = docker.build "Docker Jenkins"
    
        stage "publish"
        app.push 'master'
        app.push "${commit_id}"
    }

