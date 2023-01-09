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
                sh 'docker login -u ddarshi97 -p Devops@979'
                sh 'docker tag tomcat_build:2.0 darshh/tomcat:2.0'
                sh 'docker push darshh/tomcat:2.0'
            }
        } 
        stage( 'my deploy' ) {
        agent {label 'deploy'} 
            steps {
               sh 'docker pull darshh/tomcat:2.0'
               sh 'docker rm -f tomcat'
               sh 'docker run -d -p 8081:8080 --name tomcat darshh/tomcat:2.0'
            }
        }    
    } 
}

