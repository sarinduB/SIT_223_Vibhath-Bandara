pipeline {
    agent any
    triggers {
        pollSCM('H/2 * * * *') // Polls the SCM every 2 minutes for changes
    }
    environment {
        EMAIL_RECIPIENT = 'youremail@example.com'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the code...'
                echo 'Using Maven for building the project.'
                // Example: sh 'mvn clean install'
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
                        emailext body: "Unit and Integration Tests completed",
                                 recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                                 subject: "Unit and Integration Tests ${currentBuild.currentResult}",
                                 to: "${env.EMAIL_RECIPIENT}"
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
                        emailext body: "Security Scan completed",
                                 recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                                 subject: "Security Scan ${currentBuild.currentResult}",
                                 to: "${env.EMAIL_RECIPIENT}"
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
