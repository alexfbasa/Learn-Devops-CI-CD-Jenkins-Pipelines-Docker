# Jenkinsfile
alexsimple/docker-nodejs-demo

folder misc 
Jenkinsfile
```groovy
node {
   def commit_id  // Global variable
   stage('Preparation') {  // First Step
     checkout scm  // Plugin git
     sh "git rev-parse --short HEAD > .git/commit-id"  // it will run the git command and save the output into a file              
     commit_id = readFile('.git/commit-id').trim()   // it will read the file without space and save into the global variable
   }
   stage('test') {
     nodejs(nodeJSInstallationName: 'nodejs') {  // it will define the node installation from the Jenkins Global Config
       sh 'npm install --only=dev'
       sh 'npm test'
     }
   }
   stage('Build image') {
     dockerImage = docker.build("alexsimple/docker-nodejs-demo:${commit_id}") // it will save the docker image name as repository and commit tag
   }
   stage('docker build/push') {
     docker.withRegistry('https://registry-1.docker.io/v2/', 'dockerhub') {
       def app = docker.build("alexsimple/docker-nodejs-demo:${commit_id}", '.').push()
     }
   }
}
```