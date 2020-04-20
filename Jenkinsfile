pipeline {
  agent any
  stages{
    stage('Build'){
	  steps {
	    sh 'mvn clean package'
	  }
	  post {
	    success {
		  echo 'archiving'
		  archiveArtifatcs artifacts:'webapp/target/*war'
		}
	  }
	}
  }
}
