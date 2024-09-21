pipeline {
    agent {
        docker {
            image 'node:16'  // Use Node.js 16 Docker image as the build agent
            label 'docker'
        }
    }
    environment {
        SNYK_TOKEN = credentials('SNYK_TOKEN')  // Use the Snyk token stored in Jenkins credentials
    }
    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies...'
                    sh 'npm install --save'  // Install project dependencies
                }
            }
        }
        stage('Snyk Security Scan') {
            steps {
                script {
                    echo 'Running Snyk security scan...'
                    sh 'snyk auth $SNYK_TOKEN'  // Authenticate Snyk using the token
                    sh 'snyk test'  // Run Snyk test to scan for vulnerabilities
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    echo 'Building the application...'
                    sh 'npm run build'  // Build the application
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    sh 'npm test'  // Run application tests
                }
            }
        }
    }
    post {
        failure {
            script {
                echo 'Build failed!'
            }
        }
        success {
            script {
                echo 'Build succeeded!'
            }
        }
    }
}

