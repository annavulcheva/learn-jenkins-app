pipeline {
    agent any
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
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                echo 'Running tests inside Docker container'
                script {
                    def path = "build/index.html"
                    if (fileExists(path)) {
                        echo "${path} exists."
                    } else {
                        error "${path} does not exist."
                    }
                }
                sh 'npm test'
            }
        }
    }
}
