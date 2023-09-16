pipeline {
    agent any
    environment {
        AWS_CREDENTIALS = credentials('aws_credentials')
    }
    stages {
        stage('AWS Demo') {
            steps {
                script {
                    withCredentials([
                        [
                            $class: 'AmazonWebServicesCredentialsBinding',
                            credentialsId: 'aws_credentials',
                            accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                            secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                        ]
                    ]) {
                        // Your AWS-related commands go here
                        // For example: aws s3 ls
                    }
                }
            }
        }
        stage('Building AMI') {
            steps {
                script {
                    withCredentials([
                        [
                            $class: 'AmazonWebServicesCredentialsBinding',
                            credentialsId: 'aws_credentials',
                            accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                            secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                        ]
                    ]) {
                        sh "packer init aws-ami-v1.pkr.hcl"
                        sh "packer build aws-ami-v1.pkr.hcl"
                    }
                }
            }
        }
    }
}
