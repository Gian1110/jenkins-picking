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
                 container('kaniko') {
                    script {
                    sh 'executor --dockerfile Dockerfile --context . --destination=192.168.100.223:8083/prueba:gian --verbosity=debug'
                    echo "hola mundo ${name_container}"
                    }
                }
                  
            }
    }

    }
}