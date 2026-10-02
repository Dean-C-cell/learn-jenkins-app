pipeline {
    agent{
            docker {
                image 'mcr.microsoft.com/playwright:v1.63.0-noble'
                reuseNode true
            }
        }

    stages {
        stage('Build') {
            
            steps {
                sh '''
                ls -la
                node --version
                npm --version
                npm ci
                npm run build
                ls -la
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Test stage'
                sh '''
                test -f build/index.html
                npm test
                '''
            }
        }
        stage('E2E'){
            steps {
                sh '''
                    npx playwright test
                    echo "=== test-results ==="
                    find test-results -type f -maxdepth 2 -print
                '''
            }
        }
    }
    post {
        always{
            junit 'test-results/junit.xml'
        }
    }
}
