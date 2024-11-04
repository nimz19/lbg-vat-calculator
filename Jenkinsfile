pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // Get some code from a GitHub repository
        git branch: 'main', url: 'https://github.com/nimz19/lbg-vat-calculator.git'
      }
    }
    stage('SonarQube Analysis') {
      environment {
        scannerHome = tool 'sonarqube'
      }
      steps {
        withSonarQubeEnv('sonar-qube-13') {
          sh "${scannerHome}/bin/sonar-scanner"
          
        }

      timeout(time: 10, unit: 'MINUTES'){
        waitForQualityGate abortPipeline: true
       }

      }
    }
  }
}
