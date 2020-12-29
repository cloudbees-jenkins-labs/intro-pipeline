pipeline {
  agent {
    label 'jdk10'
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