pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
                sh 'cp appspec.yml build'
                sh 'cp -r scripts build'
                sh 'zip -r build.zip build'
                sh 'ls -la'
                sh 'pwd'
            }
        }
        stage('S3 Upload') {
            steps {
                withAWS(region: 'us-east-1', credentials: '9dc47d93-f065-48df-9d1e-562ac8922093') {
                    sh 'ls -la'
                    sh 'aws s3 cp build.zip s3://jensk-1/'
                }
            }
        }
        stage('Deploy with CodeDeploy') {
            steps {
                sh 'aws deploy create-deployment --application-name sk-angular \
                    --deployment-group-name angular-jenkins \
                    --s3-location bucket=jensk-1,key=build.zip,bundleType=zip'
            }
        }
    }
}
