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
  stage ('DAST') {
    sh 'ssh -o StrictHostKeyChecking=no kolawoleo@34.125.32.102 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://34.125.95.251/" '
  }
}
