pipeline{
    agent any
    
    environment{
        DIRECTORY_PATH = 'Deakin/SIT_223'
        TESTING_ENVIRONMENT = 'AmazingTestEnv'
        PRODUCTION_ENVIRONMENT = 'Vibhath_Bandara'
    }
    stages{
        stage('Build'){
            steps {
                echo "fetch the source code from the directory path specified by the environment variable: $DIRECTORY_PATH"
                
                echo "compile the code and generate any necessary artifacts"
            }
        }
        stage('Test'){
            steps {
                echo "running unit tests"
                echo "running integration tests"
            }
        }
        stage('Code Quality Check'){
            steps {
                echo "checking the quality of the code"
            }
        }
        stage('Deploy'){
            steps {
                echo "deploy the application to the testing environment specified by the environment variable: $TESTING_ENVIRONMENT"
            }
        }
        stage('Approval'){
            steps {
                echo "waiting for manual approval..."
                sleep 10
                echo "approval received."
            }
        }
        stage('Deploy to Production'){
            steps {
                echo "deploy the code to the production environment: $PRODUCTION_ENVIRONMENT"
            }
            
        }
    }
}
