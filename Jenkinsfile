pipeline {

  agent {
    label 'master'
  }

  stages {
    //Stage # 1
    stage('say-hello') {
      steps {
        echo "Hello ${params.Name}!"
        sh 'java -version'
      }
    }
    //Stage # 2
    stage('deploy') {
      options {
        timeout(time: 30, unit: 'SECONDS')
      }
      input {
        message 'Which version to deploy?'
        ok 'Deploy'
        parameters {
          choice(name: 'APP_VERSION', choices: "v1.1\nv1.2\nv1.3", description: 'Please, select the version of the application you want to deploy:')
        }
      }
      steps {
        echo "Deploying ${APP_VERSION} from ${env.BRANCH_NAME} branch."
      }
    }
    //Stage # 3
    stage('get-kernel') {
      steps {
        script {
          try {
            KERNEL_VERSION = sh (script: "uname -r", returnStdout: true)
          } catch(err) {
            echo "CAUGHT ERROR: ${err}"
            throw err
          }
        }
      }
    }
    //Stage # 4
    stage('say-kernel') {
      steps {
        echo "The current kernel version is ${KERNEL_VERSION}"
      }
    }
  }

  // Environment Variables
  environment {
    MY_NAME = 'Mary Magdalene'
  }

  parameters {
    string(name: 'Name', defaultValue: 'a random person', description: 'What shall I call you?')
  }

  //Post Action: guaranteed to run at the end of a Pipeline’s execution
  //Handles some notification or other steps to perform finalization, notification, or other end-of-Pipeline tasks.
  post{
    always{
      echo "Job excuted.\nJob Name:${env.JOB_NAME}\nBuild Number: ${env.BUILD_NUMBER}"
    }
    success{
      //the build has no compilation errors 
      mail  body: "Hi User, The Job ${env.JOB_NAME} - ${env.BUILD_NUMBER} ran successfully. Thanks, Jenkins Admin.", 
            charset: 'UTF-8', 
            mimeType: 'text/plain',  
            subject: "Successful Run of Pipeline: ${currentBuild.fullDisplayName}", 
            to: "8045022866@vtext.com";
      echo 'The text message has been sent to the specified user.'
    }
    unstable{
      //the build had some errors but they were not fatal
      echo '\u26A0\uFE0F The build is unstable.'
    }
    failure{
      //the build had a fatal error.
      mail  bcc: '', 
            body: "Hi User,<br>There has been a <b>Build Failure</b>. Please, find the details below:<br><br><b>Project:</b> ${env.JOB_NAME} <br><b>Build Number:</b> ${env.BUILD_NUMBER} <br><b>Build URL:</b> ${env.BUILD_URL}<br><br>Thanks,<br>Jenkins Admin", 
            cc: '', 
            charset: 'UTF-8', 
            mimeType: 'text/html', 
            replyTo: 'noreply@jenkins.com', 
            subject: "Failed Pipeline: ${currentBuild.fullDisplayName} ", 
            to: "mailmeatshraddha@gmail.com";
      echo 'The email has been sent to the specified user.'
    }
    changed{
      //only run the steps in post if the current Pipeline’s or stage’s run has a different completion status from its previous run.
      echo 'Something has been changed in the build.'
    }
    aborted{
      //the build was interrupted before it reaches its expected end
      echo '\u20E0 The build has been aborted.'
    }
  }
}
