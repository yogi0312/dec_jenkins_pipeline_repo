pipeline {
    agent any
    parameters {
        booleanParam( name: 'DEPLOY', description: 'Want to deploy to production') 
        // This parameter isn’t used in the stages but can control pipeline flow based on user input.
    }
    environment {
        CURRENT_ENV = 'prod' // Set the environment variable to 'prod' for testing purposes
    }
    stages {
        stage('stage1 when branch is main') {
            when {
                branch 'main' // This stage will only run if the current branch is 'main'
            } 
            steps {
                echo "This is stage 1 when branch is main running"
                sh '''
                    sleep 5
                    exit 1
                '''
            }
        }
        stage('when environment is prod') {
            when {
                environment name: 'CURRENT_ENV', value: 'prod' 
                // This stage will run only if the CURRENT_ENV environment variable is set to 'prod'
            } 
            steps {
                echo "This is ENVIRONMENT VARIABLE SET TO PROD STAGE running"
                sh 'sleep 5'
            }
        }
        stage('when parameter') {
            when { 
                expression {parameters.DEPLOY == true} // This stage will only run if the DEPLOY parameter is true
            } 
            steps {
                echo "This is DEPLOY PARAMETER is TRUE STAGE running"
                sh 'sleep 5'
            }
        }
    }
}