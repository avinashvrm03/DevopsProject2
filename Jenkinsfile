pipeline {
  agent any 
  tools {
    jdk 'java21'
    nodejs 'node16'
  }
  environment{
    scannerHome = tool 'SonarQube-Scanner'
    DOCKER_USER = 'avinash0001'
    APP = 'amazonprimeclone'
    IMAGE_NAME = "${Docker_User}/${App}"
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
    stage('Build And Push Docker Image') {
      steps {
        script {
          sh 'echo $IMAGE_NAME'
          docker.withRegistry('', 'dockerhub') {
            docker_image = docker.build('$IMAGE_NAME')
          }
          docker.withRegistry('', 'dockerhub') {
            sh 'echo $docker_image'
            docker_image.push('latest')
          }
        }
      }
    }
  }
}
