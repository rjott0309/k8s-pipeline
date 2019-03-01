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
                            docker build . -t ee-dtr.sttproductions.de/sttproductions/webapp/k8s-webapp:${env.BUILD_ID}
                            docker login -u devjenkins -p jenkins ee-dtr.sttproductions.de
                            docker image push ee-dtr.sttproductions.de/sttproductions/webapp/k8s-webapp:${env.BUILD_ID}
                            """
                            }
                }
        }
}
}