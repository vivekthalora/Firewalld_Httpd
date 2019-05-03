// Jenkinsfile
node("master") {
  String credentialsId = 'AWS-Jenkins-Integration'
  def environment = "Development"
  // Git checkout
  stage('checkout') {
    cleanWs()
    checkout scm
  }
}
