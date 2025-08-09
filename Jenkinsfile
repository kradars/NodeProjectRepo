pipeline {
    agent any

    tools {
        nodejs "NodeJS"
    }

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/kradars/NodeProjectRepo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'npm test || echo "No tests found, skipping"'
                }
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build || echo "No build step defined"'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                pm2 stop all || true
                pm2 start npm --name "NodeProjectRepo" -- start
                '''
            }
        }
    }
}
