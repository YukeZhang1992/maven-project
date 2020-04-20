pipeline {
  agent any 
  stages{
    stage('Build'){
	  sh 'mvn clean package'
	}
	post{
	  success{
	    echo 'artifacts archive'
		archiveArtifatcs artifacts:'**/target/*.war'
	  }
	}
  }
}