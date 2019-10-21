pipeline{
    agent{
        kubernetes {
            image 'node:6-alpine'
            args '-p 3000:3000'
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages{
        stage("Build"){
            steps {
                sh 'npm install'
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
        stage("Test") {
            steps {
                sh 'echo "Hello"'
                sh 'npm test'
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