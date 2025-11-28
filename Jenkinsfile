pipeline {
    agent any
    environment {
        BUILD_FILE_NAME = 'build'
    }
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests inside Docker container'
                sh '''
                    grep index.html $BUILD_FILE_NAME
                '''
            }
        }
    }
}
