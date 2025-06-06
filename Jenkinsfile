pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        CODEBUILD_PROJECT = 'hello-codebuild'
        AWS_CLI_PATH='/opt/homebrew/bin/aws'
    }

    stages {
        stage('Trigger AWS CodeBuild') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'aws-creds',
                    usernameVariable: 'AWS_ACCESS_KEY_ID',
                    passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                )]) {
                    withEnv([
                        "AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}",
                        "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}",
                        "AWS_REGION=${AWS_REGION}"
                    ]) {
                        sh '''
                            $AWS_CLI_PATH configure set aws_access_key_id $AWS_ACCESS_KEY_ID
                            $AWS_CLI_PATH configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
                            $AWS_CLI_PATH configure set region $AWS_REGION
                            $AWS_CLI_PATH codebuild start-build --project-name $CODEBUILD_PROJECT --region $AWS_REGION
                        '''
                    }
                }
            }
        }
    }
}
