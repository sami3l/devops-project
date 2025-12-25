pipeline {
    agent any

    tools {
        // This tells Jenkins to use the scanner tool we set up in the "Global Tools"
        // Make sure the name 'sonar-scanner' matches what you typed in the settings!
        'org.jenkinsci.plugins.sonar.SonarRunnerInstallation' 'sonar-scanner'
    }

    stages {
        stage('Code Checkout') {
            steps {
                // Just a debug message to confirm we started
                echo 'Checking out code from GitHub...'
            }
        }

        stage('Static Code Analysis') {
            steps {
                echo 'Running SonarQube Scanner...'
                // This connects to the 'sonar-server' we configured in System Settings
                withSonarQubeEnv('sonar-server') {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker Image...'
                // This uses the "Docker inside Docker" trick we set up
                sh 'docker build -t my-node-app:v1 .'
            }
        }
    }
}