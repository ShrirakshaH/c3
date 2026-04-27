pipeline {
    agent any
    tools {
        maven 'Maven3'
    }
    stages {
        stage('CHECKOUT') {
            steps {
                // Clean the workspace first to avoid old folder confusion
                cleanWs()
                git branch: 'main', url: 'https://github.com/ShrirakshaH/c3.git'
            }
        }
        stage('Build') {
            steps {
                // We move into demo and run Maven in one block
                dir('demo') {
                    bat 'mvn clean install'
                }
            }
        }
        stage('Test') {
            steps {
                dir('demo') {
                    bat 'mvn test'
                }
            }
        }
    }
    post {
        always {
            // This matches the ID you created in Manage Jenkins -> System
            slackSend (
                tokenCredentialId: 'slack-token', 
                channel: '#all-raksha',
                color: currentBuild.currentResult == 'SUCCESS' ? 'good' : 'danger',
                message: "Build ${env.JOB_NAME} - #${env.BUILD_NUMBER}: ${currentBuild.currentResult}"
            )
        }
    }
}
