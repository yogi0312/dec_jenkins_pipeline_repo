pipeline {
    agent any
    environment {   // (env works at both pipeline level and stage level)
        DOCKER_USER = 'yogesh'
        AWS_ACCESS_KEY = '64614164161641'
        }
    stages {
        stage('stage1') { 
            steps {
                // echo "DOCKER_USER: ${DOCKER_USER}"
                // echo "AWS_ACCESS_KEY: ${AWS_ACCESS_KEY}"
                echo "DOCKER_USER: ${env.DOCKER_USER}"       //Using to check whether it will support env. or what
                echo "AWS_ACCESS_KEY: ${env.AWS_ACCESS_KEY}" //Using to check whether it will support env. or what
                echo "STAGE: ${env.STAGE}"
                sh '''
                    env
                '''
                }
            }
            stage('stage2') {
                environment { // (To check whether env works at stage level also)
                    STAGE = 'STAGE1'
                }
            steps {
                echo "DOCKER_USER: ${env.DOCKER_USER}" 
                echo "AWS_ACCESS_KEY: ${env.AWS_ACCESS_KEY}"
                echo "STAGE: ${env.STAGE}"
                sh '''
                    env
                '''
                }
            }
        }
    }