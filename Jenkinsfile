pipeline {
  agent any

  tools {
    nodejs 'NodeJS 18'
    allure 'Allure'
  }

  environment {
    HOME = "${env.WORKSPACE}"
    CI = 'true'
    
  }

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/jincyraju123/PlaywrightninzaCampaign.git', branch: 'main'
      }
    }

    stage('Install Dependencies') {
      steps {
        bat 'npm ci'
        bat 'npm run install:browsers'
      }
    }

    stage('Run Tests') {
      steps {
       bat 'npm run campaigntest'
      }
      
    }

    

    stage('Generate Allure Report') {
      steps {
        bat 'npx allure generate ./allure-results -o ./allure-report --clean'
      }
    }
  }
  post {
    always {
      allure([
        reportBuildPolicy: 'ALWAYS',
        includeProperties: false,
        jdk: '',
        results: [[path: 'allure-results']]
      ])
    }

    
  }
}
