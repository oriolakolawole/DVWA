node {
  stage('SCM') {
    checkout scm
  }
  stage('Git Secrets') {
    sh 'trufflehog https://github.com/oriolakolawole/DVWA.git || true'
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'Sonar-scanner';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
   stage ('DAST Analysis') {
         sshagent (credentials:[‘sshlogin’]){
          Sh ‘ssh -o StrictHostKeyChecking=no root@35.188.206.16 "docker run -t owasp/zap2docker-stable zap-baseline.py -t https://aopartnersdev.com.ng/devsecops/" || true'    
    }
}
