pipeline {
    agent any

    stages {
        stage('STAGE-BUILD') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
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
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh 'test -f build/index.html'
                sh 'npm --version'
                sh 'npm test'
                sh 'ls -la'
                sh 'test -f lin-ne.txt'
                sh 'find . -name "lin-ne.txt"'
            }
        }
        stage('STAGE-DEPLOY'){
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps{
                sh '''
                    npm install netlify-cli
                    node_modules/.bin/netlify --version
                '''
            }
        }
    }

    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
}