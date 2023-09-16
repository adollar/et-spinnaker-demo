pipeline {
    agent any
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
