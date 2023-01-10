pipeline {
    agent {label 'build'}
    stages {
        stage('my Build') {
            steps {
                sh 'docker build -t tomcat_build:2.0 .'
            }
        }  
        stage('publish stage') {
            steps {
                sh 'docker login -u sushbsush -p Sush@98765'
                sh 'docker tag tomcat_build:2.0 sushbsush/tomcat:2.0'
                sh 'docker push sushbsush/tomcat:2.0'
            }
        } 
        stage( 'my deploy' ) {
        agent {label 'deploy'} 
            steps {
               sh 'docker pull sushbsush/tomcat:2.0'
               sh 'docker rm -f tomcat'
               sh 'docker run -d -p 8081:8080 --name tomcat sushbsush/tomcat:2.0'
            }
        }    
    } 
}

