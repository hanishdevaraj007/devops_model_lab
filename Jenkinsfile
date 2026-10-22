
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

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-cicd-app:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                    docker rm -f devops-cicd-container || true
                    docker run -d --name devops-cicd-container -p 8080:80 devops-cicd-app:latest
                '''
            }
        }

        stage('Verify Application') {
            steps {
                sh '''
                    sleep 3
                    docker exec devops-cicd-container \
                        wget -q -O /dev/null http://localhost/
                '''
                echo 'Application verification successful.'
            }
        }
    }
}
