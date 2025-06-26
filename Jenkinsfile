pipeline { 

    environment { 

        registry = "sandeepwalvekar/python3" 

        registryCredential = 'DockerHub' 

        dockerImage = '' 

    }

    agent any 

    stages { 

        stage('Building our image') { 

            steps { 

                script { 

                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 

                }

            } 

        }

        stage('Push Docker image') { 

            steps { 

                script { 

                    docker.withRegistry( '', registryCredential ) { 

                        dockerImage.push() 

                    }

                } 

            }

        } 
        
        stage('Deploy Image') {
            steps {
                sh '''
                docker stop dac-demo
                docker rm dac-demo
                docker run --name dac-demo -p 80:80 -d sandeepwalvekar/python3:$BUILD_NUMBER
                '''
            }    
        }
        
    }

}
