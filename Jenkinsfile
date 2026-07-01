pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.52.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    node --version
                    npm --version

                    npm ci
                    npx playwright install --with-deps
                '''
            }
        }

        stage('Run Tests') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.52.0-jammy'
                    reuseNode true
                }
            }
            steps {
                sh 'npm run test:regression'
            }
        }
    }
}