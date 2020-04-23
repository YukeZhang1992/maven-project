pipeline{
  agent any

  tools {
    maven 'MAVEN_HOME'
}
  stages{
    stage('build'){
      steps{
        sh 'mvn clean package'
        sh "docker build . -t tomcatwebapps:${env.BUILD_ID}"
}
}

}

}
