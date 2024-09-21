pipeline {
    agent {
        docker {
            image 'node:16'
        }
    }
    environment {
        SNYK_TOKEN = credentials('SNYK_TOKEN')  // Access the Snyk token stored in Jenkins credentials
    }
    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    echo 'Installing dependencies...'
                    sh 'npm install --save'
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
                    sh 'npm run build'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    sh 'npm test'
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

