@Library('jenkins-libs') _
pipeline {
  agent { 
        kubernetes {
            apiVersion: v1
kind: Pod
metadata:
  labels:
    jenkins/agent-type: kaniko
  namespace: devops-tools-ns
spec:
  securityContext:
    runAsUser: 1000
  containers:
  - name: jnlp
    image: jenkins/inbound-agent:latest
    imagePullPolicy: IfNotPresent
    securityContext:
      privileged: true
    resources:
      requests:
        memory: "512Mi"
        cpu: "500m"
      limits:
        memory: "1024Mi"
        cpu: "1000m"
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug
    imagePullPolicy: IfNotPresent
    command:
      - /busybox/sleep
      - infinity
    tty: true
    resources:
      requests:
        memory: "2048Mi"
        cpu: "2000m"
      limits:
        memory: "4096Mi"
        cpu: "3000m"
    securityContext:
      privileged: true
    volumeMounts:
      - name: docker-config
        mountPath: /kaniko/.docker/
  - name: kubectl
    image: bitnami/kubectl:latest
    imagePullPolicy: IfNotPresent
    command:
      - cat
    tty: true
  volumes:
  - name: docker-config
    secret:
      secretName: docker-config
        }
   }
 parameters {
    
    //server values
        string(name: 'remoteHost', defaultValue: '192.168.100.173', description: 'dns o ip del host')
        string(name: 'imagenVersion', defaultValue: '1.0.0', description: 'version de la applicacion')
        
    }
    environment {
        // container values
        name_container = 'picking'
        puerto_imagen = '5000'
        path_proyect = './'
          
    }
    stages {
        stage('existe version actual') {
            steps {
                 
                  script {
                    def parameterMap = [:]
                        parameterMap["remoteHost"] = params.remoteHost
                        parameterMap["containerName"] = name_container
                        parameterMap["branchName"] = params.imagenVersion
                    env.equalsVersion = dockerb.dockerVersionContainer(parameterMap);
                }
                
            }
        }

        // stage('Checkout on release') {
        //     when {
        //         expression {
        //             return env.equalsVersion == "false";
        //         }
        //     }
        //     steps {
        //         script {
                    
        //             def parameterMap = [:]
        //             parameterMap["imagenVersion"] = params.imagenVersion
        //             gitJob.checkoutBranch(parameterMap);

        //         }
        //     }
        // }

        // stage('docker build and push') {
        //     when {
        //         expression {
        //             return env.equalsVersion == "false";
        //         }
        //     }
        //     steps {
        //         script{
        //                 def parameterMap = [:]
        //                 parameterMap["path"] = path_proyect
        //                 parameterMap["containerName"] = name_container
        //                 parameterMap["imagenVersion"] = params.imagenVersion
        //                 dockerb.dockerBuildPush(parameterMap);
        //         }                                     
        //     }
        // }
        
        // stage('ssh pull') {
        //     when {
        //         expression {
        //             return env.equalsVersion == "false";
        //         }
        //     }
        //     steps {
        //         script{
        //                 def parameterMap = [:]
        //                 parameterMap["remoteHost"] = params.remoteHost
        //                 parameterMap["containerName"] = name_container
        //                 parameterMap["imagenVersion"] = params.imagenVersion
        //                 dockerb.dockerPull(parameterMap);
                            
        //             }
                    
        //         }  
            
        // }

        // stage('ssh rm and run') {
        //     when {
        //         expression {
        //             return env.equalsVersion == "false";
        //         }
        //     }
        //     steps {
        //         script{

        //             def parameterMap = [:]
        //             parameterMap["remoteHost"] = params.remoteHost
        //             parameterMap["containerName"] = name_container
        //             parameterMap["imagenVersion"] = params.imagenVersion
        //             parameterMap["containerPuert"] = puerto_imagen
        //             dockerb.dockerRmRun(parameterMap);
                    
        //             }
        //         }  
            
        // }
    }

    }
