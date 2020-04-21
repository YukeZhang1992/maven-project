pipeline {
  agent any
  
  tools{
    maven 'MAVEN_HOME'	
	}
	
  stages{
    stage('package'){
	  steps{
	    sh 'mvn clean package'
	  }
	  post{
	    success {
		  echo 'archiving...'
		  archiveArtifacts artifacts:'**/target/*.war'
		}
	  }
	}
	
	stage('deploy-to-stage'){
	  steps{
	    build job:'deploy-to-stage'
	  }
	}
	
	stage('deploy-to-prod'){
	  steps{
	    timeout(time:5, unit:'DAYS'){
		  input message:'are you sure that you want to deploy to prod?'		
		}
	    build job:'deploy-to-prod'
	  }
	  
	  post{
	    success {
		  echo 'deployed successfully'
		}
		
		failure {
		  echo 'deployment failed'
		}
	  }
	}
  }
}
