// Jenkinsfile
pipeline {
  //String credentialsId = 'AWS-Jenkins-Integration'
  agent any
  stages {
    // Git checkout
    stage ('Get Git Repo') {
      steps {
	git branch: 'master',
	credentialsId: 'Git-Terraform-SSH',
	url: 'https://github.com/vivekthalora/Firewalld_Httpd.git'
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
