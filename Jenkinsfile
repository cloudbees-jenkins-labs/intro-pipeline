pipeline {
  agent {
    label 'master'
  }
  stages {
    stage('say-hello') {
      steps {
        echo "Hello ${MY_NAME}!"
        echo "User Name: ${TEST_USER_USR}"
        echo "Password: ${TEST_USER_PWD}"
        sh 'java -version'
      }
    }

  }
  environment {
    MY_NAME = 'Mary Magdalene'
    TEST_USER = credentials('test-user')
  }
}