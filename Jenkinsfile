pipeline {
    agent {
        docker {
            image 'node:20'
            reuseNode true
        }
    }

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Install Playwright Browsers') {
            steps {
                sh 'npx playwright install'
            }
        }

        stage('Run Regression Tests') {
            steps {
                sh 'npm run test:regression'
            }
        }
    }
}