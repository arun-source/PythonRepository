pipeline {
	agent any
	    stages {
	        stage('Clone Repository') {
	        /* Cloning the repository to our workspace */
	        steps {
	        checkout scm
	        }
	   }
	   stage('Build docker Image') {
	        steps {
	        sh 'docker build -t mymlmodel:v1 .'
	        }
	   }
	   stage('Deploy ML Model AS Docker Container In Docker Deployment Server') {
	        steps {
		  sshagent(['Docker_Dev_Server_SSH']) {
			  
		    sh 'ssh -o StrictHostKeyChecking-no ubuntu@172.31.14.22 docker rm -f mlmodelcontainer || true'
			  
		    sh 'ssh -o StrictHostKeyChecking-no ubuntu@172.31.14.22 docker run -d -p 5000:4000 --name mlmodelcontainer mymlmodel:v1'
			  
		  //  sh ' docker run -d -p 5000:4000 --name nlpmodel mynlpmodel:v1'	  
    
                      }
	        }
	   } 
	   stage('Testing'){
	        steps {
	            echo 'Testing..'
	            }
	   }
    }
}
