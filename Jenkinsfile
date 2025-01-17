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
                sh 'rm -fr html'
                sh 'git clone https://github.com/inestmimi4/firstPipeline.git'
            }
        }
        stage('Push repo to remote host') {
            steps {
                echo 'Connecting to remote host and pulling down the latest version...'
                sh 'ssh -i ~/working.pem ec2-user@35.176.182.32 sudo git -C /var/www/html pull'
            }
        }
        stage('Check website is up') {
            steps {
                echo 'Checking if the website is up...'
                sh 'curl -Is 35.176.182.32 | head -n 1'
            }
        }
    }
}