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
                 container(name:'kaniko', shell: '/busybox/sh') {
                    script {
                    sh 'chmod -R 755 /home/jenkins/agent/workspace'
                    sh '#!/busybox/sh'
                    sh '/kaniko/executor --dockerfile Dockerfile --context . --destination=192.168.100.223:8083/prueba:gian'
                    echo "hola mundo ${name_container}"
                    }
                }
                  
            }
    }

    }
}