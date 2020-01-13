pipeline {
  agent {
    node {
      label 'build'
    }
  }

  triggers {
    pollSCM('H/15 * * * *')
  }

  stages {
    stage('Start') {
      steps {
        bitbucketStatusNotify(buildState: 'INPROGRESS')
      }
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

