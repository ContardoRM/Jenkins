node("docker") {
      docker.withRegistry('https://hub.docker.com/r/contardorm/jenkins/', 'docker-hub-credentials') {
        git url: "https://github.com/ContardoRM/Jenkins.git", credentialsId: 'git-hub-credentials'
    
       sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
      def app = docker.build "docker_jenkins"
    
            
        stage "run"
      def app = docker.run "docker_jenkins"
      //stage "publish"
      //  app.push 'master'
       // app.push "${commit_id}"
            
      }
    }

