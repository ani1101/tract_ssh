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
          sh ('script/trigger_codedeploy.sh')
      }
    }
  }
  post {
    success {
      script {
        buildTag = BUILD_TAG.replace('%2F', '/')
        jobName = JOB_NAME.replace('%2F', '/')
        currentBuild.result = "SUCCESS"
      }
      echo "Project ${jobName}, build ${BUILD_ID} successful"
    }

    failure {
      script {
        buildTag = BUILD_TAG.replace('%2F', '/')
        jobName = JOB_NAME.replace('%2F', '/')

        if (currentBuild.result != "ABORTED") {
          currentBuild.result = "FAILURE"
        }
      }

      echo "Project ${jobName}, build ${BUILD_ID} failed"


      mail (
        body: "<b>Build Failed</b><br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br>URL of build: ${env.BUILD_URL}",
        charset: 'UTF-8',
        mimeType: 'text/html',
        subject: "ERROR CI: Project name -> ${env.JOB_NAME}",
        to: "anirudh.rana@careerbuilder.com"
      )
    }
  }
}

