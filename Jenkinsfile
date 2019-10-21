pipeline{
    agent{
    kubernetes {
      defaultContainer 'node'
    }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages{
        stage("Build"){
            steps{
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