pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''echo Building
env'''
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
      }
    }
  }
}