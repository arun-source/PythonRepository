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
	        sh 'docker build -t 111992/mymlmodel:v1 .'
	        }
	   }
             stage('Docker Login and Push') {
	        steps {
		withCredentials([string(credentialsId: 'HUB_Credential', variable: 'Hubpwd')]) {
			sh 'docker login -u 111992 -p ${Hubpwd}'	
                     }	
		     sh 'docker push 111992/mymlmodel:v1'
	        }
	   }		    
		    
		    
	   stage('Deploying Container In Docker Deployment Server') {
	        steps {
		  sshagent(['Docker_Dev_Server_SSH']) {
			  
		    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.14.22 docker rm -f mlmodelcontainer || true'
			  
		    sh 'ssh -o StrictHostKeyChecking=no ubuntu@172.31.14.22 docker run -d -p 8080:4000 --name mlmodelcontainer 111992/mymlmodel:v1'
			  
		  //  sh ' docker run -d -p 5000:4000 --name nlpmodel mynlpmodel:v1'	  
    
                      }
	        }
	   } 
	  stage('Sending Email'){
	        steps {
	        emailext body: '''Hi Team,
                Regards,
                Arun Kumar''', subject: 'Send Email', to: 'yarunkumar92@gmail.com'
	          }
	   }
    }
}
