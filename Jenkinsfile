pipeline {
  agent any 
  tools {
    jdk 'jav21'
    nodejs 'node14'
  }
  environment{
    Scanner_Home = tool 'SonarQube-Scanner'
  }
  stages {
    stage('Cleanup WorkSpace') {
      steps {
        cleanupWs()
      }
    }
  }
}
