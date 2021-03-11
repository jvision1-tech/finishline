pipeline { 
    environment { 
        registry = "jvision1/coker-boutique" 
        registryCredential = 'dockerhub-connection' 
        dockerImage = '' 
    }
    agent any 
    stages { 
       stage('Building our image') { 
            steps { 
               dir ('/var/lib/jenkins/workspace/coker-boutique_website/Statiswebserver1') { 
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
    }
}