pipeline {
    agent any

    stages {
        stage('Hello') {
            agent{
                docker{
                    image 'node:18-alpine'
                }
            }
            steps {
                sh 'npm --version'
                sh 'npm install'
                sh 'npm run build'
                sh 'test -d build'
            }
        }
    }
}