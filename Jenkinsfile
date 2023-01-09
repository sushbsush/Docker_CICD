pipeline {
    agent {label 'slavebuild'}
    stages {
        stage('my Build') {
            steps {
                sh "echo ${BUILD_VERSION}"
                sh 'docker build -t tomcat_build:${BUILD_VERSION} --build-arg BUILD_VERSION=${BUILD_VERSION} .'
            }
        }  
        stage('publish stage') {
            steps {
                sh "echo ${BUILD_VERSION}"
                sh 'docker login -u madhusudhanpk -p 116007App@
                sh 'docker tag tomcat_build:${BUILD_VERSION} madhusudhanpk/tomcat:${BUILD_VERSION}'
                sh 'docker push madhusudhanpk/tomcat:${BUILD_VERSION}'
            }
        } 
        stage( 'my deploy' ) {
        agent {label 'slaverun'} 
            steps {
               sh 'docker pull madhusudhanpk/tomcat:${BUILD_VERSION}'
               sh 'docker rm -f tomcat'
               sh 'docker run -d -p 8085:8080 --name tomcat madhusudhanpk/tomcat:${BUILD_VERSION}'
            }
        }    
    } 
}

