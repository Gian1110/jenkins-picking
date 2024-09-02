@Library('jenkins-libs') _
pipeline {
  agent { 
        kubernetes {
            yaml k8sAgentConfig()
        }
   }

    environment {
        // container values
        name_container = 'picking'
          
    }
    stages {
        stage('existe version actual') {
            steps {
                 
                  script {
                    sh 'docker build .'
                    echo "hola mundo ${name_container}"
                }
                
            }
    }

    }
}