// Jenkinsfile
pipeline {
  //String credentialsId = 'AWS-Jenkins-Integration'
  agent any
  parameters {
    //booleanParam(name: 'skipOneView', description: 'Skip the OneView stage?', defaultValue: false)
    booleanParam(name: 'skipOneView', description: 'Skip the OneView stage?')
    string(name: 'SSHuser', description: 'Remote SSH username')
  }
  stages {
    // Git checkout
    stage ('Get Git Repo') {
      steps {
	git branch: 'master',
	credentialsId: 'Git-Terraform-SSH',
	url: 'https://github.com/vivekthalora/Firewalld_Httpd.git'
      }
    }
    // SSH remote connect and execute commands
    stage ('Executing commands remotely via SSH') {
      steps{
        expression {
          params.skipOneView == false
        }
        sshagent(credentials : ['Ansible_SSH_PrivateKey']) {
          sh 'ssh -o StrictHostKeyChecking=no lnxcfg@ansible-svr01 uptime'
          //sh 'ssh -v ansible-svr01'
          sh 'scp /var/lib/jenkins/workspace/Ansible-Http-Firewalld/README.md lnxcfg@ansible-svr01:/home/lnxcfg'
	  sh 'ls -ltra .'
	  sh 'file ./firewalld.yml'
	}
      }
    }
    // SSH remote connect and execute commands
    stage ('Running Ansible Playbook Remotely') {
      steps{
        sshagent(credentials : ['Ansible_SSH_PrivateKey']) {
	  sh "pwd" 
          //sh 'ssh -o StrictHostKeyChecking=no lnxcfg@ansible-svr01 ansible-playbook ./firewalld.yml -i ./hosts'
          sh "ssh -o StrictHostKeyChecking=no lnxcfg@ansible-svr01 -C \"ansible-playbook ./firewalld.yml -i ./hosts\""
        } 
      }     
    }
  } 
}
