pipeline {
    agent any
    options {
        disableConcurrentBuilds()
    }
    triggers {
        pollSCM('* * * * *') // Polls the SCM every minute
    }
    stages {
        stage('Clone the repo') {
            steps {
                echo 'Cloning the repository...'
                bat '''
                if exist html (
                    rmdir /S /Q html
                )
                git clone https://github.com/inestmimi4/firstPipeline.git
                '''
            }
        }
        stage('Push repo to remote host') {
            steps {
                echo 'Connecting to remote host and pulling down the latest version...'
                bat '''
                if exist C:\\path\\to\\working.pem (
                    ssh -i C:\\path\\to\\working.pem ec2-user@35.176.182.32 sudo git -C /var/www/html pull
                ) else (
                    echo "Pem file not found, skipping SSH step."
                )
                '''
            }
        }
        stage('Check website is up') {
            steps {
                echo 'Checking if the website is up...'
                bat 'curl -Is 35.176.182.32 | head -n 1'
            }
        }
    }
}