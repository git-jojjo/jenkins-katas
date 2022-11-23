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
            sh 'ci/build-app.sh'
            echo 'echo "Hello"'
          }
        }

      }
    }

    stage('archive artifacts') {
      steps {
        archiveArtifacts 'app/build/libs'
      }
    }

  }
  environment {
    Hello = 'Hello'
  }
}