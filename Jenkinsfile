pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
                sh 'ls'
                sh 'cd build'
                sh 'ls'
            }
        }
        stage('S3 Upload') {
            steps {
                withAWS(region: 'us-east-1', credentials: '96cd3f7a-fd9d-4dfc-81ea-925377ac392e') {
                    sh 'ls -la'
                    sh 'aws s3 cp build s3://sk-reactjs/'
                }
            }
        }
    }
}
