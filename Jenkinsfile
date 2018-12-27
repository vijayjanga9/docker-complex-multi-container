pipeline {
    agent none    
    stages {
        
    	stage('Build Images') {
    	    agent any
                steps {
                    sh 'docker build -t ravi2krishna/multi-client ./client'
                    sh 'docker build -t ravi2krishna/multi-nginx ./nginx'
                    sh 'docker build -t ravi2krishna/multi-server ./server'
                    sh 'docker build -t ravi2krishna/multi-worker ./worker'
                }
            }
            
        stage('Push Images') {
    	    agent any
                steps {
                    withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
                    sh 'docker push ravi2krishna/multi-client'
                    sh 'docker push ravi2krishna/multi-nginx'
                    sh 'docker push ravi2krishna/multi-server'
                    sh 'docker push ravi2krishna/multi-worker'
                  
                    }
                }
            }	

    }
}
