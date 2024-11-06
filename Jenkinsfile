pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building the project...'
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // تثبيت Node.js
                    sh 'npm install -g newman'
                    // تثبيت Newman's htmlextra reporter
                    sh 'npm install -g newman-reporter-htmlextra'
                    // إنشاء دليل newman
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
