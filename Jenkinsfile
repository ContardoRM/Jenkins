node("docker") {
      docker.withRegistry('https://hub.docker.com/r/contardorm/jenkins/', 'docker-hub-credentials') {
        git url: "https://github.com/ContardoRM/Jenkins.git", credentialsId: 'git-hub-credentials'
    
       sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
      def app = docker.build "contardorm/jenkins"
    
        stage ('Run Application') {
          // Start database container here
      // sh 'docker run -d --name db -p 8091-8093:8091-8093 -p 11210:11210 arungupta/oreilly-couchbase:latest'

      // Run application using Docker image
         sh "docker run --name docker-stage -d -p 8000:8000 contardorm/jenkins"
            }
            
     //   stage "publish"
    //    app.push 'master'
     //  app.push "${commit_id}"
            
      }
    }

