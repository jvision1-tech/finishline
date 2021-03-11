pipeline { 
    environment { 
        registry = "jvision1/coker-boutique" 
        registryCredential = 'dockerhub-connection' 
        dockerImage = '' 
    }
    agent any 
    stages { 
        stage('Cloning our Git') { 
            steps { 
                git 'https://github.com/jvision1-tech/finishline.git' 
            }
        } 
        stage('Building our image') { 
            steps { 
               sh 'cd Staticwebserver1' 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
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
    }
}