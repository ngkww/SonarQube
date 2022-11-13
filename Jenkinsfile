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
        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=." "-Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqp_a3497e4d56dfec3c9357c25e877d9bf517b57a85"

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