pipeline {
  agent any
  
  tools{
    maven 'local maven'
  }
  
  parameters{
    string(name:'tomcat_stage', defaultValue:'3.80.155.110', description:'stage tomcat')
    string(name:'tomcat_prod', defaultValue:'34.203.28.8', description:'prod tomcat')
  }
  
  triggers{
    pollSCM(* * * * *)
  }
  
  stages{
    stage('Build'){
	  steps{
	    bat mvn clean package
	  }
	  post{
	    success{
		echo 'archiving'
		archiveArtifacts artifacts:'**/target/*.war'
		}
	  }
	}
	
	stage('deployment'){
	  parallel{
	    stage('deploy-to-stage'){
		  steps{
		    bat 'scp -i D:/yukiko/cmder/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_stage}:/var/lib/tomcat8/webapps'
		  }
		}
	    stage('deploy-to-prod'){
		  steps{
		    bat 'scp -i D:/yukiko/cmder/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat8/webapps'
		  }
		}	
	  }
	}
  }
}
