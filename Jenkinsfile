pipeline {
  agent {
    node {
      label 'master'
    }
  }

  triggers {
    pollSCM('H/15 * * * *')
  }
   parameters {
     choice(name: 'Ready to start the build?',
       choices: 'Proceed\nAbort',
       description: 'For security')
   }
   stages {
    stage('Install and Build') {
      steps {
          sh ('script/build.sh')
      }
    }
    stages {
     stage('push docker image') {
       steps {
           docker.withRegistry("https://467883107641.dkr.ecr.eu-west-1.amazonaws.com", "ecr:us-east-1:CredentialId('ad803b9c-11dc-43b2-9fad-c3548722f082')") {
           docker.image("ecart-staging").push()
	    }
    stage('DEPLOY') {
      steps {
          sh ('script/trigger_codedeploy.sh')
      }
    }
  }
}

