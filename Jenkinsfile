@Library('jenkins-libs') _
pipeline {
  agent any
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

        stage('Checkout on release') {
            steps {
                script {
                    
                    def parameterMap = [:]
                    parameterMap["imagenVersion"] = params.imagenVersion
                    gitJob.checkoutBranch(parameterMap);

                }
            }
        }
        stage('existe version actual') {
            steps {
                script {
                    def parameterMap = [:]
                        parameterMap["remoteHost"] = params.remoteHost
                        parameterMap["containerName"] = name_container
                        parameterMap["imagenVersion"] = params.imagenVersion
                    env.equalsVersion = dockerb.dockerVersionContainer(parameterMap);
                }
            }
        }

        stage('prueba') {
            when {
                expression {
                    echo "${equalsVersion}"
                    return env.equalsVersion;
                }
            }
            steps {
                script {
                    echo "hola"
                }
            }
        }

        stage('docker build and push') {
            steps {
                script{
                        def parameterMap = [:]
                        parameterMap["path"] = path_proyect
                        parameterMap["containerName"] = name_container
                        parameterMap["imagenVersion"] = params.imagenVersion
                        dockerb.dockerBuildPush(parameterMap);
                }                                     
            }
        }
        stage('ssh pull') {
            steps {
                script{
                        def parameterMap = [:]
                        parameterMap["remoteHost"] = params.remoteHost
                        parameterMap["containerName"] = name_container
                        parameterMap["imagenVersion"] = params.imagenVersion
                        dockerb.dockerPull(parameterMap);
                            
                    }
                    
                }  
            
        }

        stage('ssh rm and run') {
            steps {
                script{

                    def parameterMap = [:]
                    parameterMap["remoteHost"] = params.remoteHost
                    parameterMap["containerName"] = name_container
                    parameterMap["imagenVersion"] = params.imagenVersion
                    parameterMap["containerPuert"] = puerto_imagen
                    dockerb.dockerRmRun(parameterMap);
                    
                    }
                }  
            
        }
    }

    }
