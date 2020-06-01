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
	/*   stage('Run Image') {
	        steps {
	        sh 'sudo docker run -d -p 5000:4000 --name nlpmodel mynlpmodel:v1'
	        }
	   } */
	   stage('Testing'){
	        steps {
	            echo 'Testing..'
	            }
	   }
    }
}
