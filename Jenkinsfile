node {
  stage('Retrieving') {
    
  }
  stage('Searching for Secrets') {
    sh 'trufflehog https://github.com/oriolakolawole/DVWA.git || true'
  }
  stage('Static Application Security Testing') {
    def scannerHome = tool 'Sonar-scanner';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
   stage ('Dynamic Application Security Testing') {
      sh 'sudo docker run -t owasp/zap2docker-stable zap-baseline.py -t https://aopartnersdev.com.ng/devsecops/ || true '  
   }
}
