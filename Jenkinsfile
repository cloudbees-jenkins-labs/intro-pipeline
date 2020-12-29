pipeline {
  agent {
    label 'master'
  }
  stages {
    stage('say-hello') {
      steps {
        echo "Hello ${MY_NAME}!"
        echo "User Name: ${TEST_USER_USR}"
        echo "Password: ${TEST_USER_PSW}"
        sh 'java -version'
      }
    }

  }
  environment {
    MY_NAME = 'Mary Magdalene'
    TEST_USER = credentials('113bed98-0426-43bd-967a-d3a11f10084a')
  }
}