// Jenkinsfile
pipeline {
  //String credentialsId = 'AWS-Jenkins-Integration'
  def environment = "Development"

  stages {

    // Git checkout
    stage ('checkout') {
      cleanWs()
      checkout scm
    }

    // SSH remote connect and execute commands
    stage ('Deploy') {
      sshagent(credentials : ['Ansible_SSH_PrivateKey']) {
        sh 'ssh -o StrictHostKeyChecking=no lnxcfg@ansible-svr01 uptime'
        sh 'ssh -v ansible-svr01'
        //sh 'scp ./source/filename lnxcfg@ansible-svr01:/remotehost/target'
      }
    }

  }
}
