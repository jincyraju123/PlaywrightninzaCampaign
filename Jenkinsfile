pipeline {
  agent any

  tools {
    nodejs 'NodeJS 18'
    allure 'Allure'
  }

  environment {
    HOME = "${env.WORKSPACE}"
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

    stage('Process Allure Results') {
      steps {
        bat 'npx allure-playwright'           //Converts Playwright output into Allure-friendly format
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
