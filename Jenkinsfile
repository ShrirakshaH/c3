pipeline {
    agent any
    tools {
        maven 'Maven3'
    }
    stages {
        stage('CHECKOUT') {
            steps {
                // Point this to your C3 repository
                git branch: 'main', url: 'https://github.com/ShrirakshaH/c3.git'
            }
        }
        stage('Build') {
            steps {
                // If your pom.xml is sitting in the root of C3, remove the dir('demo') wrapper
                // If you have a 'demo' folder inside C3, keep it like this:
                dir('demo'){
                    bat 'mvn clean install'
                }
            }
        }
        stage('Test') {
            steps {
                dir('demo'){
                    bat 'mvn test'
                }
            }
        }
    }
}
