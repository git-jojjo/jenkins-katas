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
            }

          }
          steps {
            echo 'Hello'
            sh 'ci/build-app.sh'
          }
        }

      }
    }

  }
  environment {
    Hello = 'Hello'
  }
}