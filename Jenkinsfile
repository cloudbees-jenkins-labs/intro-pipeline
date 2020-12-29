pipeline {
  agent {
    label 'master'
  }
  stages {
    stage('say-hello') {
      steps {
        echo "Hello ${MY_NAME}!"
        sh 'java -version'
      }
    }

  }
  environment {
    MY_NAME = 'Mary Magdalene'
  }
}