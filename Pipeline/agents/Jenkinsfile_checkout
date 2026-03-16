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
        stage('CHECKOUT_REPO') {
            steps {
                checkout ([ $class: 'GitSCM',
                branches: [[name: '*/main']], 
                extensions: [], 
                userRemoteConfigs: [[credentialsId: 'yogi-git-jen', url: 'https://github.com/yogi0312/dec_jenkins_pipeline_repo.git']]
                // This step checks out the code from the specified Git repository and branch using the provided credentials.
                ])
               sh '''
                    echo GIT_BRANCH: $GIT_BRANCH
                    echo BRANCH_NAME: $BRANCH_NAME
                '''
            }
                
        }
        
        stage('stage1 when branch is main') {
            when {
                expression {
                    return env.GIT_BRANCH == 'origin/main'
                }
            } 
            steps {
                echo "This is stage 1 running"
                sh '''
                    pwd
                    ls -lrt
                    sleep 5
                '''
            }
        }
        stage('when environment') {
            when {
                environment name: 'CURRENT_ENV', value: 'prod' 
                // This stage will run only if the CURRENT_ENV environment variable is set to 'prod'
            } 
            steps {
                echo "This is ENVIRONMENT VARIABLE SET TO PROD STAGE running"
                sh '''
                    pwd
                    ls -lrt
                    sleep 5
                '''
            }
        }
        stage('when parameter') {
            when { 
                expression {params.DEPLOY == true} // This stage will only run if the DEPLOY parameter is true
            } 
            steps {
                echo "This is DEPLOY PARAMETER is TRUE STAGE running"
                sh 'sleep 5'
            }
        }
    }
}