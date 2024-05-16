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
                withAWS(region: 'us-east-1', credentials: 'f2980eb1-8312-47c1-9835-b406849f32ba') {
                    sh 'ls -la build'
                    sh 'aws s3 cp build s3://sk-reactjs/' --recursive
                }
            }
        }
    }
}
