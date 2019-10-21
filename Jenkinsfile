pipeline {
  agent {
    kubernetes {
      label 'jenkins-nodejs'
      defaultContainer 'nodejs'
    }
  }
  environment {
    CI = 'true'
  }
  options {
    skipStagesAfterUnstable()
  }
  stages {
    stage("Build"){
      steps {
        sh 'npm install'
      }
      post {
        always{
          echo "========always========"
        }
        success{
          echo "========A executed successfully========"
        }
        failure{
          echo "========A execution failed========"
        }
      }
    }
    stage('Test') {
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
    stage("Package") {
      steps {
        container('docker') {
          sh "docker ps"
        }
      }
    }
  }
}