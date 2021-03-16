pipeline { 
    environment { 
        registry = "jvision1/coker-boutique" 
        registryCredential = 'dockerhub-connection' 
        dockerImage = '' 
        AWS_ACCESS_KEY_ID     = credentials('aws_jenkins-access')
        AWS_SECRET_ACCESS_KEY = credentials('aws_jenkins-access')
        AWS_DEFAULT_REGION = ('us-east-1')
    }
    agent any 
    stages { 
       stage('Building our image') { 
            steps { 
               dir ('Statiswebserver1') { 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                  }
                }
            } 
        }
        stage('Deploy our image') { 
            steps { 
                script { 
                    docker.withRegistry( '', registryCredential ) { 
                        dockerImage.push() 
                    }
                } 
            }
        } 
        stage('Cleaning up') { 
            steps { 
                sh "docker rmi $registry:$BUILD_NUMBER" 
            }
        } 
        stage('Cloudformation') {
            steps {
              dir ('Statiswebserver1') {  
                sh "aws cloudformation create-stack --template-body 'file:///docker-cft.yaml' --stack-name 'docker-compose' --region 'us-east-1' --parameter ParameterKey=KeyName,ParameterValue=finishlinelab ParameterKey=InstanceType,ParameterValue=t2.micro
"
            }
        }
    }
}