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
            post{
                mail to: EMAIL_RECIPIENT
                subject: "Build Status Email"
                body: "Build was successful"
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                echo 'Using JUnit for unit testing and TestNG for integration tests.'
                // Example: sh 'mvn test'
            }
            post {
                always {
                    script {
                        emailext(
                            body: """<p>Unit and Integration Tests have completed.</p>
                                    <p>Status: ${currentBuild.currentResult}</p>""",
                            subject: "Unit and Integration Tests: ${currentBuild.currentResult}",
                            to: "${env.EMAIL_RECIPIENT}",
                            attachLog: true
                        )
                    }
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                echo 'Using SonarQube for code analysis.'
                // Example: sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan...'
                echo 'Using OWASP Dependency-Check for security scanning.'
                // Example: sh 'dependency-check --scan ./'
            }
            post {
                always {
                    script {
                        emailext(
                            body: """<p>Security Scan has completed.</p>
                                    <p>Status: ${currentBuild.currentResult}</p>""",
                            subject: "Security Scan: ${currentBuild.currentResult}",
                            to: "${env.EMAIL_RECIPIENT}",
                            attachLog: true
                        )
                    }
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                echo 'Deploying to AWS EC2 instance for staging.'
                // Example: sh 'scp target/app.war ec2-user@staging-server:/path/to/deploy'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                echo 'Using Postman or Selenium for integration testing on staging.'
                // Example: sh 'run-integration-tests.sh'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                echo 'Deploying to AWS EC2 instance for production.'
                // Example: sh 'scp target/app.war ec2-user@production-server:/path/to/deploy'
            }
        }
    }
}
}
