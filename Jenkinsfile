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
                withAWS(region: 'us-east-1', credentials: '02872160-3518-4c1b-b05f-10c0d6373614') {
                    sh 'ls -la build'
                    sh 'aws s3 cp build s3://sk-reactjs/ --recursive'
                }
            }
        }
    }
}
