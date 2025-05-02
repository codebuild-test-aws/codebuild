pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        CODEBUILD_PROJECT = 'hello-codebuild'
    }

    stages {
        stage('Trigger AWS CodeBuild') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'aws-creds', 
                    usernameVariable: 'AWS_ACCESS_KEY_ID', 
                    passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                )]) {
                    sh """
                        aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
                        aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
                        aws configure set region $AWS_REGION
                        aws codebuild start-build --project-name $CODEBUILD_PROJECT --region $AWS_REGION
                    """
                }
            }
        }
    }
}
