//node("docker") {
 //     docker.withRegistry('https://hub.docker.com/r/contardorm/jenkins/', 'docker-hub-credentials') {
 //       git url: "https://github.com/ContardoRM/Jenkins.git", credentialsId: 'git-hub-credentials'
    
 //       sh "git rev-parse HEAD > .git/commit-id"
 //       def commit_id = readFile('.git/commit-id').trim()
  //      println commit_id
    
        //stage "build"
      //def app = docker.build "docker_jenkins"
    
  //      stage "publish"
   //     app.push 'master'
  //      app.push "${commit_id}"
            
//      }
//    }

node {
    def app

    stage('Clone repository locally') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }
}

node('docker') {

    stage('Clone repository on slave') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm

    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("csuttles/hsl")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://hub.docker.com/r/contardorm/jenkins/', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
