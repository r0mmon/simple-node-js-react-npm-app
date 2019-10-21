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
      agent {
        kubernetes {
          label 'jenkins-docker'
        }
      }
      steps {
        container('docker') {
          sh "docker ps"
        }
      }
    }
    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input message: 'Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }
  }
}