pipeline {
    agent any

    parameters {
        string(name: 'STACK_NAME', defaultValue: 's3-stack-2', description: 'CloudFormation Stack Name')
        string(name: 'TEMPLATE_FILE', defaultValue: 'jenkins-bucket.yml', description: 'CloudFormation Template File')
        string(name: 'BUCKET_NAME', defaultValue: 'sandhya-bucket-2', description: 'S3 Bucket Name')
        choice(name: 'REGION', choices: ['us-east-1', 'us-west-1', 'ap-south-1'], description: 'AWS Region')
    }

    environment {
        AWS_DEFAULT_REGION = "${params.REGION}"
    }

    stages {
        stage('Checkout Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Sandhya-AR/jenkins-bucket-cloudformation-template.git'
            }
        }

        stage('Deploy S3 Stack') {
            steps {
                script {
                    echo "Running CloudFormation deployment for S3..."
                    sh """
                        aws cloudformation deploy \
                          --stack-name ${params.STACK_NAME} \
                          --template-file ${params.TEMPLATE_FILE} \
                          --region ${params.REGION} \
                          --parameter-overrides BucketName=${params.BUCKET_NAME}
                    """
                }
            }
        }
    }
}
