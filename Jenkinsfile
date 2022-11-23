pipeline {
  agent any
  stages {
    stage('stage1') {
      parallel {
        stage('stage1') {
          steps {
            sh 'echo "hello world"'
          }
        }

        stage('build-app') {
          agent {
            docker {
              image 'gradle:6-jdk11'
              args 'ci/build-app.sh'
            }

          }
          steps {
            echo 'Hello'
          }
        }

      }
    }

  }
  environment {
    Hello = 'Hello'
  }
}