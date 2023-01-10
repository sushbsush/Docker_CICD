pipeline {
    agent {label 'build'}
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
                withCredentials([usernamePassword(credentialsId: 'Dockerhub', passwordVariable: 'DockerhubPassword', usernameVariable: 'DockerhubUser')]) {
                sh "docker login -u ${env.DockerhubUser} -p ${env.DockerhubPassword}"
                sh 'docker tag tomcat_build:${BUILD_VERSION} sushbsush/tomcat:${BUILD_VERSION}'
                sh 'docker push sushbsush/tomcat:${BUILD_VERSION}'
                }
            }
        } 
        stage( 'my deploy' ) {
        agent {label 'deploy'} 
            steps {
               sh 'docker pull sushbsush/tomcat:${BUILD_VERSION}'
               sh 'docker rm -f tomcat'
               sh 'docker run -d -p 8081:8080 --name tomcat sushbsush/tomcat:${BUILD_VERSION}'
            }
        }    
    } 
}
