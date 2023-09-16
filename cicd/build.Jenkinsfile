pipeline {
  agent any
  stages {
    stage('docker build') {
      steps {
        container('dind') {
          sh 'docker version'
        }
      }
    }
  }
}
