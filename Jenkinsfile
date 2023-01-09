pipeline {
    agent {label 'slavebuild'}
    stages {
        stage('my Build') {
            steps {
               
                sh 'docker build -t tomcat_build:2.0 .'
            }
        }  
        stage('publish stage') {
            steps {
                
                sh 'docker login -u madhusudhanpk -p 116007App@'
                sh 'docker tag tomcat_build:2.0 madhusudhanpk/tomcat:2.0'
                sh 'docker push madhusudhanpk/tomcat:2.0'
            }
        } 
        stage( 'my deploy' ) {
        agent {label 'slaverun'} 
            steps {
               sh 'docker pull madhusudhanpk/tomcat:2.0'
               sh 'docker rm -f tomcat'
               sh 'docker run -d -p 8085:8080 --name tomcat madhusudhanpk/tomcat:2.0'
            }
        }    
    } 
}

