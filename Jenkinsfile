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
                            docker build . -t rjo-dtr.lab.capstonec.net/randy/nginx:k8s-${env.BUILD_ID}
                            docker login -u randy -p Number3! rjo-dtr.lab.capstonec.net
                            docker image push rjo-dtr.lab.capstonec.net/randy/nginx:k8s-${env.BUILD_ID}
                            """
                            }
                }
        }
}
}
