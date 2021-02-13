pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws_jenkins-access')
        AWS_SECRET_ACCESS_KEY = credentials('aws_jenkins-access')
        AWS_DEFAULT_REGION = ('us-east-1')
    }
    stages {
        stage('Cloudformation') {
            steps {
                sh "aws cloudformation create-stack --template-body 'file:///var/lib/jenkins/workspace/second-ci-pipeline_Finishlinelab4/finishlinelab4/finishlinelab4infra.yaml' --stack-name 'finishlinlab4' --region 'us-east-1' --parameter ParameterKey=KeyName,ParameterValue=finishlinelab ParameterKey=InstanceType,ParameterValue=t2.micro"
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
