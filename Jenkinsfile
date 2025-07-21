pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')         // Replace with your Jenkins credentials ID
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key') // Replace with your Jenkins credentials ID
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {
        stage('Download CloudFormation Template') {
            steps {
                script {
                    sh 'curl -o jenkins-bucket.yml https://raw.githubusercontent.com/Sandhya-AR/jenkins-bucket-cloudformation-template/main/jenkins-bucket.yml'
                }
            }
        }

        stage('Deploy CloudFormation Stack') {
            steps {
                script {
                    sh '''
                      aws cloudformation deploy \
                      --template-file jenkins-bucket.yml \
                      --stack-name my-s3-bucket-stack \
                      --capabilities CAPABILITY_NAMED_IAM \
                      --region ap-south-1
                    '''
                }
            }
        }
    }
}

