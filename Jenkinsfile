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
                    sh 'executor --dockerfile /home/jenkins/agent/workspace/picking/Dockerfile --context . --destination=192.168.100.223:8083/prueba:gian'
                    echo "hola mundo ${name_container}"
                    }
                }
                  
            }
    }

    }
}