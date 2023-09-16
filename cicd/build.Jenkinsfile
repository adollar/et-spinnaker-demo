pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: docker
            image: docker:latest
            command:
            - cat
            tty: true
            volumeMounts:
             - mountPath: /var/run/docker.sock
               name: docker-sock
          volumes:
          - name: docker-sock
            hostPath:
              path: /var/run/docker.sock
        '''
    }
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-creds')
  }
  stages {
    stage('Docker login') {
      steps {
        container('docker') {
          sh '''
              echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
          '''
        }
      }
    }
    stage('Docker build') {
      steps {
        container('docker') {
          sh '''
              docker build . -t hpkns/spinnaker-demo:${HashCommit}
          '''
        }
      }
    }
    stage('Docker push') {
      steps {
        container('docker') {
          sh '''
              docker push hpkns/spinnaker-demo:${HashCommit}
          '''
        }
      }
    }
  }
}
