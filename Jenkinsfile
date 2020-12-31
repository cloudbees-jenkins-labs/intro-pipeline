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
            body: "<b>Failure</b><br>\n\<br>Project: ${env.JOB_NAME} 
                  <br>Build Number: ${env.BUILD_NUMBER} 
                  <br> URL de build: ${env.BUILD_URL}", 
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


pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                sh 'echo "Fail!"; exit 1'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            mail  bcc: '', 
                  body: "<b>Example</b><br>\n\<br>Project: ${env.JOB_NAME} 
                        <br>Build Number: ${env.BUILD_NUMBER} 
                        <br> URL de build: ${env.BUILD_URL}", 
                  cc: '', 
                  charset: 'UTF-8', 
                  from: '', 
                  mimeType: 'text/html', 
                  replyTo: '', 
                  subject: "ERROR CI: Project name -> ${env.JOB_NAME}", 
                  to: "foo@foomail.com";
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}