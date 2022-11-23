pipeline {
  agent any
  stages {
    stage('Clown down'){
      agent {
        label 'master-label'
        }
      steps {
      stash excludes: '.git/', name: 'code'
      }

    }
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
          options {
              skipDefaultCheckout true
          }
          steps {
            unstash 'code'
            sh 'ci/build-app.sh'
            
          }
        }
         stage('test-app') {
          agent {
            docker {
              image 'gradle:6-jdk11'
            }

          }
          options {
              skipDefaultCheckout true
          }
          steps {
            unstash 'code'
            sh 'ci/unit-test-app.sh'
            junit 'app/build/test-results/test/TEST-*.xml'
          }
        }
      }
    }

    stage('archive artifacts') {
      steps {
        archiveArtifacts(artifacts: 'app/build/libs/', allowEmptyArchive: true)
      }
    }

  }
  environment {
    Hello = 'Hello'
  }
  post {
    cleanup {
        deleteDir() /* clean up our workspace */
    }
}
}
