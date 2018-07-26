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
      steps {
        sh 'echo Ready to deploy'
        unstash 'artifact.txt'
        sh 'cat artifact.txt'
      }
    }
  }
}