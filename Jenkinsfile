pipeline {

  agent {
    label 'master'
  }

  stages {
    //Stage # 1
    stage('say-hello') {
      steps {
        echo "Hello ${params.Name}!"
        echo "User Name: ${TEST_USER_USR}"
        echo "Password: ${TEST_USER_PSW}"
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
        echo "Deploying ${APP_VERSION}"
      }
    }
  }

  // Environment Variables
  environment {
    MY_NAME = 'Mary Magdalene'
    TEST_USER = credentials('abc')
  }

  parameters {
    string(name: 'Name', defaultValue: 'a random person', description: 'What shall I call you?')
  }

  //Post Action: guaranteed to run at the end of a Pipeline’s execution
  //Handles some notification or other steps to perform finalization, notification, or other end-of-Pipeline tasks.
  post{/*
    always{

    }
    success{
      //the build has no compilation errors 

    }
    unstable{
      //the build had some errors but they were not fatal

    }*/
    failure{
      //the build had a fatal error.
      mail  bcc: '', 
            body: "Hi User,<br>There has been a <b>Build Failure</b>. Please, find the details below:<br><br><b>Project:</b> ${env.JOB_NAME} <br><b>Build Number:</b> ${env.BUILD_NUMBER} <br><b>Build URL:</b> ${env.BUILD_URL}<br><br>Thanks,<br>Jenkins Admin", 
            cc: '', 
            charset: 'UTF-8', 
            from: '', 
            mimeType: 'text/html', 
            replyTo: 'noreply@jenkins.com', 
            subject: "Failed Pipeline: ${currentBuild.fullDisplayName} ", 
            to: "mailmeatshraddha@gmail.com";
    }
    /*
    changed{

    }
    aborted{
      //the build was interrupted before it reaches its expected end

    }*/
  }
}
