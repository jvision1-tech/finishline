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
                sh "aws cloudformation create-stack --template-body 'file:///var/lib/jenkins/workspace/econd-ci-pipeline_finishlinelab4/Finishlinelab4/finishlinelab4infra.yaml' --stack-name 'finishlinelab4' --region 'us-east-1' --parameter 'file://var/lib/jenkins/workspace/parameter.json'"
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
