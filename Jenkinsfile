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
                post {
                    success {
                        echo 'All build...'
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