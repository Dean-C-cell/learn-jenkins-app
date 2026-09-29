pipeline {
    agent any

    stages {
        stage('with docker') {
            agent {
                docker {
                    image 'node:18-alpine'
                }
            }
            steps {
                sh 'npm --version'
            }
        }
    }
}
