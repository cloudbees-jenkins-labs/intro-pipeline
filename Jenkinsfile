pipeline {
  agent {
    label 'master'
  }
  stages {
    stage('say-hello') {
      steps {
        echo "Hello ${params.Name}!"
        echo "User Name: ${TEST_USER_USR}"
        echo "Password: ${TEST_USER_PSW}"
        sh 'java -version'
      }
    }

    stage('deploy') {
      options {
        timeout(time: 30, unit: 'SECONDS')
      }
      input {
        message 'Shall we continue?'
      }
      steps {
        echo 'Continuing with the deployment..'
      }
    }

  }
  environment {
    MY_NAME = 'Mary Magdalene'
    TEST_USER = credentials('113bed98-0426-43bd-967a-d3a11f10084a')
  }
  parameters {
    string(name: 'Name', defaultValue: 'a random person', description: 'What shall I call you?')
  }
}