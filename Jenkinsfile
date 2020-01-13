pipeline {
  agent {
    node {
      label 'master'
    }
  }

  triggers {
    pollSCM('H/15 * * * *')
  }
 
 stage('Build on master') {
    when {
        branch "master"
    }
    stage('Install and Build') {
      steps {
        sh """
          sh script/build.sh
            .
        """
      }
    }
  }
}

