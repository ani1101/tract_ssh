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

