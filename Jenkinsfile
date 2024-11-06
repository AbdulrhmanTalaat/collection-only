pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    sh 'export PATH=$PATH:/home/jenkins/.npm-global/bin'
                    sh 'npm install -g --prefix /home/jenkins/.npm-global newman'
                    sh 'npm install -g --prefix /home/jenkins/.npm-global newman-reporter-htmlextra'
                    sh 'mkdir -p newman'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying application...'
            }
        }
    }
}
