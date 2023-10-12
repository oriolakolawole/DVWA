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
      sh 'sudo docker run -t owasp/zap2docker-stable zap-baseline.py -t https://aopartnersdev.com.ng/devsecops/ || true '  
   }
}
