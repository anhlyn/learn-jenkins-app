pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID = '12c6bd16-fc7c-440f-a1e6-8d18a4f518eb'
        NETLIFY_CLI_TOKEN = credentials('netlify-cli-token')
    }

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
                    echo "Deploying to PROD with site id: $NETLIFY_SITE_ID"
                    node_modules/.bin/netlify status
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