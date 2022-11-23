pipeline {
  agent any
  stages {
    stage('parallel execution') {
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
          }
        }

      }
    }

    stage('archive artifacts') {
      steps {
        archiveArtifacts 'app/build/libs/'
      }
    }

  }
  environment {
    Hello = 'Hello'
  }
}