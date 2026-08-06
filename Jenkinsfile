pipeline{
    agent any

    tools{
        nodejs 'Node20'
    }

    stages {
    stage('SonarQube analysis') {
      steps {
        script {
            scannerHome = tool 'sonarqube'// must match the name of an actual scanner installation directory on your Jenkins build agent
        }
        withSonarQubeEnv('mysonaqube') {// If you have configured more than one global server connection, you can specify its name as configured in Jenkins
          sh "${scannerHome}/bin/sonar-scanner"
        }
      }
    }

    stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'SECONDS') {
                waitForQualityGate abortPipeline: true
            }
        }
    }
  }
} 
