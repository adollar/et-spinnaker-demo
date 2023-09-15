pipeline {
    agent any

    stages {
        stage('Docker build') {
            steps {
                sh '''
                    echo $HashCommit
                '''
            }
        }
    }
}
