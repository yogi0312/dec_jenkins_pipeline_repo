pipeline {
    agent any
    stages {
        stage('stage1') { 
            steps {
                echo "This is stage 1 running"
                sh '''
                    sleep 5
                '''
            }
        }
        stage('PARALLEL TESTING') {
            parallel {
                stage('WINDOWS TESTING') {
                    steps {
                        echo "This is WINDOWS TESTING running"
                        sh 'sleep 5'
                    }
                }
                stage('LINUX TESTING') {
                    steps {
                        echo "This is LINUX TESTING running"
                        sh '''
                        sleep 5
                        exit 1  // (To check whether it will mark the parallel stage as failed or not) 
                    '''
                    }
                }
                stage('MAC TESTING') {
                    steps {
                        echo "This is MAC TESTING running"
                        sh 'sleep 5'
                    }
                }
            }
        }
        stage('FINAL STAGE') { 
            steps {
                echo "This is FINAL STAGE running"
                sh 'sleep 5'
                }
            }
        }
    }