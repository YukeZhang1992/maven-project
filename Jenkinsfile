pipeline {
  agent any
  tools{
	  maven 'local maven'
	}
  stages{
    stage('Build'){
	  steps {
	    bat 'mvn clean package'
	  }
	  post {
	    success {
		  echo 'archiving'
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
	        input message: 'deploy to prod?'
	      }
	      build job: 'deploy-to-prod'
      }  
      post {
	      success {
	        echo '成功しました～～'
	      }
	      failure {
	        echo '残念ながら失敗しました～～コードを丁寧に検査してもう一回試してみてください'
	      }
      }
	  }
  }
}
