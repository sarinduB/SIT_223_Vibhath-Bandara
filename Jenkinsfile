pipeline {
    agent any
    triggers {
        pollSCM('H/2 * * * *') // Polls the SCM every 2 minutes for changes
    }
    environment {
        EMAIL_RECIPIENT = 'sarindu.v.bandara@gmail.com' // Set the recipient email address
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                echo 'Using Maven for building the project.'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                echo 'Using JUnit for unit testing and TestNG for integration tests.'
            }
            post {
                always {
                    mail(
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "Unit and Integration Tests: ${currentBuild.currentResult}",
                        body: """<p>Unit and Integration Tests have completed.</p>
                                 <p>Status: ${currentBuild.currentResult}</p>"""
                    )
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                echo 'Using SonarQube for code analysis.'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                echo 'Using OWASP Dependency-Check for security scanning.'
            }
            post {
                always {
                    mail(
                        to: "${env.EMAIL_RECIPIENT}",
                        subject: "Security Scan: ${currentBuild.currentResult}",
                        body: """<p>Security Scan has completed.</p>
                                 <p>Status: ${currentBuild.currentResult}</p>"""
                    )
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                echo 'Deploying to AWS EC2 instance for staging.'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                echo 'Using Postman or Selenium for integration testing on staging.'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                echo 'Deploying to AWS EC2 instance for production.'
            }
        }
    }
}
