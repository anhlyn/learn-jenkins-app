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
                sh 'touch lin-ne.txt'
                sh 'echo "Lin test on 2 different docker images" >> lin-ne.txt'
            }
        }
        stage('STAGE-TEST'){
            steps{
                sh 'test -f build/index.html'
                sh 'ls -la'
                sh 'test -f lin-ne.txt'
            }
        }
    }
}