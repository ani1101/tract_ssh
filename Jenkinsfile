pipeline {
  agent {
    node {
      label 'master'
    }
  }

  triggers {
    pollSCM('H/15 * * * *')
  }
   stages {
    stage('Start') {
      steps {
        githubNotify(status: 'PENDING')
      }
    }
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

