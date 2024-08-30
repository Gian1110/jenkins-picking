pipeline {
    agent {
        kubernetes {
            label 'kaniko-build'
            defaultContainer 'kaniko'
            yaml '''
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-value
spec:
  containers:
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug
    command:
    - cat
    tty: true
    volumeMounts:
    - name: kaniko-secret
      mountPath: /kaniko/.docker
      readOnly: true
  - name: jenkins-agent
    image: jenkins/inbound-agent
    env:
    - name: JENKINS_URL
      value: http://jenkins-service-np.devops-tools-ns.svc.cluster.local:8080
    - name: JENKINS_AGENT_PORT
      value: "50000"
    - name: JENKINS_SECRET
      valueFrom:
        secretKeyRef:
          name: jenkins-agent-secret
          key: secret
  volumes:
  - name: kaniko-secret
    secret:
      secretName: kaniko-secret
'''
        }
    }
    stages {
        stage('Build') {
            steps {
                container('kaniko') {
                    sh '''
                    /kaniko/executor \
                      --dockerfile=/workspace/Dockerfile \
                      --context=dir:///workspace/ \
                      --destination=<your-repo>/<your-image>:<tag>
                    '''
                }
            }
        }
    }
}
