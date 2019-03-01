pipeline {
    agent any
    
    tools {
            maven 'MVN'
        }
stages{
        stage('Maven Build'){            
            steps {
                
                    sh """
                    mvn clean package
                    """

                post {
                    success {
                        junit '**/target/*.xml'
                    }
                }
            }
        }
        stage('Docker Build') {
        steps {
            container('docker') {
                            sh """
                            docker build . -t ee-dtr.sttproductions.de/sttproductions/webapp/k8s-webapp:${env.BUILD_ID}
                            """
                            }
                }
        }
}
}