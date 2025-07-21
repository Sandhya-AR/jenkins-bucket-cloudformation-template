pipeline {

    agent any
 
    environment {

        AWS_DEFAULT_REGION = 'ap-south-1'

        STACK_NAME = 's3-bucket-stack'

        TEMPLATE_PATH = "jenkins-bucket.yml"

    }
 
    stages {

        stage('Clone Git Repo') {

            steps {

                git url: 'https://github.com/Sandhya-AR/jenkins-bucket-cloudformation-template.git', branch: 'main'

            }

        }
 
        stage('Deploy CloudFormation Stack') {

            steps {

                script {

                    if (!fileExists("${TEMPLATE_PATH}")) {

                        error "CloudFormation template not found at: ${TEMPLATE_PATH}"

                    }
 
                    sh """

                        aws cloudformation deploy \

                          --template-file "${TEMPLATE_PATH}" \

                          --stack-name "${STACK_NAME}" \

                          --region "${AWS_DEFAULT_REGION}" \

                          --capabilities CAPABILITY_NAMED_IAM

                    """

                }

            }

        }

    }
 
    post {

        success {

            echo "✅ CloudFormation stack deployed successfully."

        }

        failure {

            echo "❌ CloudFormation stack deployment failed."

        }

    }

}
 
