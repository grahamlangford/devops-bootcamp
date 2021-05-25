pipeline {
    agent any
    tools {
        nodejs 'node-12.16.1'
        // 'hudson.plugins.sonar.SonarRunnerInstallation' 'GrahamScanner'
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
                withCredentials([usernamePassword(credentialsId: 'ECRAccess', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                    sh '''
                        wget https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                        dpkg -i ./docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                        apt-get update
                        apt-get install -y awscli
                        docker build -t workshopuser3:latest .
                        docker tag workshopuser3:latest workshopuser3:${BUILD_NUMBER}
                        docker tag workshopuser3:latest 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser3:latest
                        $(aws ecr get-login --region us-east-1 | sed 's/-e none//g')
                        docker push 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser3:latest
                    '''
                }
            }
        }
    }
}