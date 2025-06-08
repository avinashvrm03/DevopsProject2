pipeline {
  agent any 
  tools {
    jdk 'java21'
    nodejs 'node16'
  }
  environment{
    Scanner_Home = tool 'SonarQube-Scanner'
  }
  stages {
    stage('Cleanup WorkSpace') {
      steps {
        cleanWs()
      }
    }
  }
}
