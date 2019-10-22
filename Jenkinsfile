pipeline {
  agent {
    kubernetes {
      label 'build-service-pod'
      defaultContainer 'nodejs'
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    job: build-service
spec:
  containers:
  - name: nodejs
    image: node
    command: ["cat"]
    tty: true
  - name: docker
    image: docker:18.09.2
    command: ["cat"]
    tty: true
    volumeMounts:
    - name: docker-sock
      mountPath: /var/run/docker.sock
  volumes:
  - name: docker-sock
    hostPath:
      path: /var/run/docker.sock
"""
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
        container('nodejs') {
          sh "npm run-script build"
        }
        container('docker') {
          sh "docker ps"
          sh "ls -l"
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