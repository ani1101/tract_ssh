pipeline {
  agent {
    node {
      label 'master'
    }
  }

  options {
    ansiColor('xterm')
    buildDiscarder(logRotator(numToKeepStr: '30', artifactNumToKeepStr: '30'))
    timeout(time: 60, unit: 'MINUTES')
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

