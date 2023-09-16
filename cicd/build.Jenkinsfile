pipeline {
    agent {
        docker {
            image 'maven:3.5.0'
        }
    stages {
        stage('Docker build') {
            container('dind') {
                steps {
                    sh '''
                        docker ps
                    '''
                }
            }

        }
    }
}
