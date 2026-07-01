pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.61.1-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    node --version
                    npm --version
                    npm ci
                '''
            }
        }

        stage('Run Playwright Tests') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.61.1-jammy'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    npm run test:regression
                    npx playwright test --reporter=html
                '''
            }
        }
    }

    post {
        always {
            publishHTML(target: [
            allowMissing: false,
            alwaysLinkToLastBuild: true,
            keepAll: true,
            reportDir: 'playwright-report',
            reportFiles: 'index.html',
            reportName: 'Playwright HTML Report'
        ])
            archiveArtifacts artifacts: 'playwright-report/**', allowEmptyArchive: true
            archiveArtifacts artifacts: 'test-results/**', allowEmptyArchive: true
            archiveArtifacts artifacts: 'allure-results/**', allowEmptyArchive: true
        }
    }
}