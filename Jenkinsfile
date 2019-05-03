// Jenkinsfile
node("master") {
  //String credentialsId = 'AWS-Jenkins-Integration'
  def environment = "Development"
  // Git checkout
  stage('checkout') {
    cleanWs()
    checkout scm
  }
  stage ('Deploy') {
    steps{
      sshagent(credentials : ['Ansible_SSH_PrivateKey']) {
        sh 'ssh -o StrictHostKeyChecking=no lnxcfg@ansible-svr01 uptime'
        sh 'ssh -v ansible-svr01'
        //sh 'scp ./source/filename lnxcfg@ansible-svr01:/remotehost/target'
      }
    }
  }
}
