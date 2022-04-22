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
     when {
            expression {
                GIT_BRANCH = sh(returnStdout: true, script: 'git rev-parse --abbrev-ref HEAD').trim()
                return !(GIT_BRANCH == 'main')
            }
        }
        steps {
            echo 'Do stuff/deploy.'
        }
    }
  }
}
