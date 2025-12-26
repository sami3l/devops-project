pipeline {
    agent any

    // We keep this to ensure the tool is installed
    tools {
        // This tells Jenkins to use the scanner tool we set up in the "Global Tools"
        // Make sure the name 'sonar-scanner' matches what you typed in the settings!
        'hudson.plugins.sonar.SonarRunnerInstallation' 'sonar-scanner'
    }

    stages {
        stage('Code Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Static Code Analysis') {
            steps {
                script {
                    // TEACHER NOTE: This command asks Jenkins "Where did you install the tool named 'sonar-scanner'?"
                    // It saves the path into the variable 'scannerHome'
                    def scannerHome = tool 'sonar-scanner'
                    
                    // Now we run the command using the FULL PATH so there is no confusion
                    withSonarQubeEnv('sonar-server') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker Image...'
                sh 'docker build -t my-node-app:v1 .'
            }
        }
    }
}
