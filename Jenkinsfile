pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''echo Building
echo Build number $BUILD_NUMBER > artifact.txt'''
        stash 'artifact.txt'
      }
    }
    stage('Test') {
      parallel {
        stage('Test Java 8') {
          agent {
            label 'jdk8'
          }
          steps {
            sh 'java -version'
          }
        }
        stage('Test Java 9') {
          agent {
            label 'jdk9'
          }
          steps {
            sh 'java -version'
          }
        }
      }
    }
    stage('Deploy') {
      options {
        timeout(time: 10, unit: 'SECONDS')
      }
      steps {
        checkpoint 'deploy'
        input 'Proceed with deployment?'
        unstash 'artifact.txt'
        sh 'cat artifact.txt'
      }
    }
  }
  post {
    aborted {
      echo 'Timed out waiting for approval'

    }

  }
}