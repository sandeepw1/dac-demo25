pipeline { 

    environment { 

        registry = "sandeepwalvekar/python3" 

        registryCredential = 'DockerHub' 

        dockerImage = '' 

    }

    agent any 

    stages { 

        stage('Cloning our Git') { 

            steps { 

                git 'https://github.com/sandeepw1/dac-demo25.git' 

            }

        } 

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
        

        stage('Cleaning up') { 

            steps { 

                sh "docker rmi $registry:$BUILD_NUMBER" 

            }

        } 

    }

}
