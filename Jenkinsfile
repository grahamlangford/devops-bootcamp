pipeline {
    agent any
    tools {
        nodejs 'node-12.16.1'
        'hudson.plugins.sonar.SonarRunnerInstallation' 'GrahamScanner'
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'npm test'
            }
        }

        stage('Sonar Scan') {
            steps {
                echo 'Running SonarQube Scan'
                sh '/var/jenkins_home/tools/hudson.plugins.sonar.SonarRunnerInstallation/GrahamScanner/bin/sonar-scanner'
            }
        }
    }
}