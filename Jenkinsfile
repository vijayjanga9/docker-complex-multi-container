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

	stage('Deploy AWS') {
            agent any
                steps {
                    step([$class: 'AWSEBDeploymentBuilder', applicationName: 'multi-docker', awsRegion: 'us-east-1', bucketName: 'elasticbeanstalk-us-east-1-256225485494', checkHealth: true, credentialId: 'multi-docker-deployer', environmentName: 'MultiDocker-env', excludes: '', includes: '', keyPrefix: '', maxAttempts: 5, rootObject: '', sleepTime: 90, versionDescriptionFormat: 'mapp', versionLabelFormat: 'multi-app', zeroDowntime: false])    
                }
            } 
    }
}
