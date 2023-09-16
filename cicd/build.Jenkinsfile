pipeline {
  agent any
  stages {
    stage('docker build') {
      steps {
        container('docker') {
          sh 'docker ps'
        }
      }
    }
  }
}
