pipeline {
    agent any

    stages {
        stage('STAGE-BUILD') {
            agent{
                docker{
                    image 'node:18-alpine'
                }
            }
            steps {
                sh 'npm --version'
                sh 'npm ci'
                sh 'npm run build'
            }
        }
        stage('STAGE-TEST'){
            agent{
                docker{
                    image 'node:18-alpine'
                }
            }
            steps{
                sh 'test -f build/index.html'
            }
        }
    }
}