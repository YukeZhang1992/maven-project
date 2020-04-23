pipeline{
  agent any

  tools {
    maven 'MAVEN_HOME'
}
  stages{
    stage('build'){
      steps{
        sh 'mvn clean package'
        sh "/usr/bin/docker build . -t tomcatwebapps:${env.BUILD_ID}"
}
}

}

}
