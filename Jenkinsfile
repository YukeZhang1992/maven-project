pipeline{
  agent any
  
  tools{
    maven 'MAVEN_HOME'
  }
  
  parameters{
    string(name:'tomcat_stage', defaultValue:'3.90.199.126', description:'stage tomcat')
    string(name:'tomcat_prod', defaultValue:'50.17.93.249', description:'prod tomcat')
  }
  
  triggers{
    pollSCM('* * * * *')
  }
  
  stages{
    stage('build'){
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

    stage('deploy'){
	  parallel{
	  stage('deploy-to-stage'){
	    steps{
		    echo "substitute for ${params.tomcat_stage}"
		}
	}
	  stage('deploy-to-prod'){
	    steps{
		  sh 'sudo su'
		  sh "scp -i /home/ec2-user/jenkins.pem  **/target/*.war  ec2-user@${params.tomcat_prod}:/home/ec2-user/downloads/apache-tomcat-8.5.54/webapps"
		}
	  }

	}
  }
  }
}
