pipeline {
  agent any 
  tools {
    jdk 'java21'
    nodejs 'node16'
  }
  environment{
    scannerHome = tool 'SonarQube-Scanner'
  }
  stages {
    stage('Cleanup WorkSpace') {
      steps {
        cleanWs()
      }
    }
    stage('Checkout Code') {
      steps {
        git branch: 'main', credentialsId: 'github', url: 'https://github.com/avinashvrm03/DevopsProject2.git'
      }
    }
    stage('SonarQube Analysis') {
      steps {
        script {
          withSonarQubeEnv('SonarQube-Server') {
             sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectName=amazonprimeclone -Dsonar.projectKey=amazonprimeclone"
          }
        }
      }
    }
    stage('Quality Gate') {
      steps {
        waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube-token'
      }
    }
    stage('Install npm') {
      steps {
        sh 'npm install'
      }
    }
    stage('Trivy FS Scan') {
      steps {
        sh 'trivy fs . > trivy.txt'
      }
    }
  }
}
