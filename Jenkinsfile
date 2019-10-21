pipeline{
    agent{
        kubernetes {
            label 'jenkins-nodejs'
            defaultContainer 'nodejs'
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages{
        stage("Build"){
            steps {
                sh 'npm build'
            }
            post{
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
            sh 'echo "Hello"'
            sh 'npm test'
          }
        }
        post {
          always {
            echo "Ok"
          }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}