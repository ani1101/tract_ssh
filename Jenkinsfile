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
    stage('DEPLOY') {
      steps {
          sh ('script/build.sh')
      }
    }
  }
}

