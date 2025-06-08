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
    stage('Checkout Code') {
      steps {
        git branch: 'main', credentailsId: 'github', url: 'https://github.com/avinashvrm03/DevopsProject2.git'
      }
    }
  }
}
