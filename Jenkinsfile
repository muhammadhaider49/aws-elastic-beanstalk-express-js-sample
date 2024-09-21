pipeline {
  agent {
    docker {
      image 'node:16'  // Use Node.js 16 Docker image as the build agent
      label 'docker'
    }
  }
  stages {
    stage('Install Dependencies') {
      steps {
        script {
          echo 'Installing dependencies...'
          sh 'npm install --save'  // Install dependencies
        }
      }
    }
    stage('Build') {
      steps {
        script {
          echo 'Building the application...'
          sh 'npm run build'  // Build step (if applicable, customize for your project)
        }
      }
    }
    stage('Test') {
      steps {
        script {
          echo 'Running tests...'
          sh 'npm test'  // Run tests (if applicable, customize for your project)
        }
      }
    }
  }
  post {
    always {
      echo 'CI/CD Pipeline complete!'
    }
  }
}
