pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate Source') {
            steps {
                sh 'test -f app/index.html'
                sh 'test -f Dockerfile'
                echo 'Source validation successful.'
            }
        }
    }
}
