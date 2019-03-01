pipeline {
    agent any
    
    tools {
            maven 'MVN'
        }
stages{
        stage('Maven Build'){            
            steps {
                container('jenkins-slave') {
                    sh """
                    mvn clean package
                    """
                }                
            }
        }
        stage('Docker Build') {
        steps {
            container('docker') {
                            sh """
                            docker build . -t YOURDTRURL/REPONAME-${env.BUILD_ID}
                            docker login -u DTRUSER -p PASSWORD ee-dtr.sttproductions.de
                            docker image push YOURDTRURL/REPONAME:k8s-${env.BUILD_ID}
                            """
                            }
                }
        }
}
}