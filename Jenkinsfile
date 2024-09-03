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
                    echo 'ls a picking'
                    sh 'ls -la /home/jenkins/agent/workspace/picking'
                    echo 'ls a pwd'
                    sh 'ls -la'
                    sh 'chmod 644 Dockerfile'
                    sh 'executor --dockerfile Dockerfile --context . --destination=192.168.100.223:8083/prueba:gian'
                    echo "hola mundo ${name_container}"
                    }
                }
                  
            }
    }

    }
}