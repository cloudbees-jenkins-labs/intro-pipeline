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
  environment {
    MY_NAME = 'Mary Magdalene'
    TEST_USER = credentials('113bed98-0426-43bd-967a-d3a11f10084a')
  }
  parameters {
    string(name: 'Name', defaultValue: 'a random person', description: 'What shall I call you?')
  }
}
