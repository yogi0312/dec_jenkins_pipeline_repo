 pipeline {
    agent any
    triggers{
        cron('H/5 * * * *')  // This line sets up a cron trigger to run the pipeline every 5 minutes.  
    }
    options {
        ansiColor('xterm')  
// This line enables ANSI color support in the console output, allowing for colored text and improved readability.        
        // timeout(time: 5, unit: 'MINUTES') 
// This line sets a timeout for the entire pipeline, specifying that it should not run for more than 5 minute. If the pipeline exceeds this time limit, it will be automatically aborted.
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
                    echo -e \033[32mListing files:
                    ls -lrt
                    sleep 5
                '''
            }
        }
    }
}