pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
  
    stages {
        stage('Init') {
            steps {
               sh """
                cd 01-vpc
                terraform init -reconfigure
               """
            }
        }
        stage('Test') {
           
            steps {
                sh """
                cd 01-vpc
                terraform test
                """
            }
        }
        stage('Deploy') {
         
            steps {
                sh """
                cd 01-vpc
                terraform apply -auto-approve
                """
            }
        }

        stage('Destroy') {
           
            steps {
                sh """
                cd 01-vpc
                terraform destroy -auto-approve
                """
            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success { 
            echo 'I will run when pipeline is success'
        }
        failure { 
            echo 'I will run when pipeline is failure'
        }
    }
}