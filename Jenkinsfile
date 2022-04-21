pipeline {
    agent any
    stages {
    stage('Install') {
      steps { bat 'npm install' }
    }

    stage('Test') {
      parallel {
        stage('Static code analysis') {
            steps { bat 'npm run-script lint' }
        }
        stage('Unit tests') {
            steps { bat 'npm run-script test -- --no-watch --no-progress --browsers=ChromeHeadlessCI' }
        }
      }
    }

    stage('Build') {
      steps { bat 'npm run-script build' }
    }
      
      stage('Deploy - Staging') {
    steps {
        sh './deploy staging'
        sh './run-smoke-tests'
    }
    }
  }
}
