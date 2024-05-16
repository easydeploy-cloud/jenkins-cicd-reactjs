pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
                sh 'ls'
                sh 'cd build'
            }
        }
        stage('S3 Upload') {
            steps {
                withAWS(region: 'us-east-1', credentials: '9dc47d93-f065-48df-9d1e-562ac8922093') {
                    sh 'ls -la'
                    sh 'aws s3 cp * s3://jensk-1/'
                }
            }
        }
    }
}
