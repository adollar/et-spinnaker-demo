pipeline {
    agent any

    stages {
        stage('Docker build') {
            steps {
                sh '''
                    export
                    echo $HashCommit
                '''
            }
        }
    }
}
