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
          steps {
            sh 'java -version'
          }
        }
        stage('Test Java 7') {
          steps {
            sh 'java -version'
          }
        }
      }
    }
    stage('Deploy') {
      options {
        timeout(time: 5, unit: 'SECONDS')
      }
      input {
        message 'Proceed with deployment?'
      }
      steps {
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