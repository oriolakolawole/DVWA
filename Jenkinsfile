node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'SonarScanner';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
  stage('Snyk Analysis') {
    snykSecurity severity: 'medium', snykInstallation: 'snykscan', snykTokenId: 'Synk', targetFile : 'compose.lock'
  }
}
