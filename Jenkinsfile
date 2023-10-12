node {
  stage('SCM') {
    checkout scm
  }
  stage('Git Secrets') {
    sh 'trufflehog https://github.com/oriolakolawole/DVWA.git --json || true'
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'Sonar-scanner';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
