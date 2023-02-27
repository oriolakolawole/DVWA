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
  stage ('ZAP Analysis') {
    sshagent(credentials:['zap']){
      sh 'ssh -o StrictHostKeyChecking=no root@34.125.32.102 "docker run -t owasp/zap2docker-stable zap-baseline.py -t http://34.125.95.251/" || true '
    }
  }
  stage('DAST') {
    parallel {
      stage('OWASP ZAP') {
        agent any
        steps {
          sh '''
            pip install archerysec-cli --force  
            mkdir /tmp/archerysec-scans-report
            archerysec-cli -h http://34.125.206.181:8000 -t 7_6iNNDlzMzXZ4Xy5kn2yqm9smWVWVyNmBP9IT1mCaQoSXUE67-Y6Wn6b2db-pDi --cicd_id=c2f1e4a2-a52c-46f4-a8f7-c914b0e35d5b --project=cb8b7c16-64d1-48ff-85a6-9b05fae347fa --zap-base-line-scan --report_path=/tmp/archerysec-scans-report/
          '''
        }
       }
     }
   }
}
