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
    stage('docker build') {
      steps {
        container('docker') {
          sh '''
              echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
              docker build . -t et/spinnaker-demo
              docker push et/spinnaker-demo:${HashCommit}
          '''
        }
      }
    }
  }
}
