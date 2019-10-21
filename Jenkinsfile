pipeline {
  agent {
    kubernetes {
      defaultContainer 'nodejs'
    }
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
    stage("Test") {
      steps {
        sh 'echo "Hello"'
        sh 'npm test'
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