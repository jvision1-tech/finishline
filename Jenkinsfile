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
  //              sh "mkdir coker"
  //              sh "cd coker" 
    //            git 'https://github.com/jvision1-tech/finishline.git' 
            }
        } 
        stage('Building our image') { 
            steps { 
               sh 'cd /var/lib/jenkins/workspace/coker-boutique_website/Staticwebserver1' 
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