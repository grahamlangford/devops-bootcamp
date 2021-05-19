pipeline {
    agent any
    tools {
        nodejs 'node-12.16.1' 
    }
    
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                sh 'npm install'
            }
        }
    }
}