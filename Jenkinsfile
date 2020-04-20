pipeline {
  agent any
  stages{
    stage('Build'){
	  steps {
	    bat 'mvn clean package'
	  }
	  post {
	    success {
		  echo 'archiving'
		  archiveArtifacts artifacts:'package/webapp/target/*war'
		}
	  }
	}
  }
}
