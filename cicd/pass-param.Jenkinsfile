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
    stage('Run end-to-end tests') {
      steps {
        container('docker') {
          sh '''
            echo "Running pass-param for hash commit ${HashCommit}..."
            echo TEST_ARG=PARAM-TO-PASS > artifact.properties
          '''
          archiveArtifacts artifacts: 'artifact.properties'
        }
      }
    }
  }
}
