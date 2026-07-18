pipeline {
    agent any

    environment{
        NETLIFY_SITE_ID = '12c6bd16-fc7c-440f-a1e6-8d18a4f518eb'
        NETLIFY_AUTH_TOKEN = credentials('netlify-cli-token')
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
                sh 'npm ci'
                sh 'npm run build'
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
                sh 'npm test'
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
                    node_modules/.bin/netlify deploy --dir=build --prod --no-build
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