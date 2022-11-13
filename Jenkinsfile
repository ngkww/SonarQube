pipeline {
   agent any 
   stages {
     stage ('Checkout') {
       steps {
          git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
        }
   }

   stage('Code Quality Check via SonarQube') {
    steps {
       script {
        def scannerHome = tool 'SonarQube';
        withSonarQubeEnv('SonarQube') {
        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP-Dsonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.login=sqp_f77998372ac39fcfc5c225f38d92b172dfb4e455"
        }
     }
   }
 }
}
post {
   always {
      recordIssues enabledForFailure: true, tool: sonarQube()
   }  
  }
}