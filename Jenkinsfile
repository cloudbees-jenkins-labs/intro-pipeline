pipeline {
  agent {
    label 'master'
  }
  stages {
    stage('say-hello') {
      steps {
        echo 'Hello world'
        sh 'java -version'
      }
    }

  }
}