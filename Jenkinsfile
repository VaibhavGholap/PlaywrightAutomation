pipeline {
    agent any

    stages {
        stage('Run Playwright Tests') {
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
                    npx playwright install
                    npm run test:regression
                '''
            }
        }
    }
}