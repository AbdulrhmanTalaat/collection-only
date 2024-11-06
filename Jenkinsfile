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

{
  "steps": [
    {
      "name": "Install Node.js",
      "uses": "actions/setup-node@v4",
      "with": {
        "node-version": "20"
      }
    },
    {
      "name": "Install Newman",
      "run": "npm install -g newman"
    },
    {
      "name": "Install htmlextra reporter",
      "run": "npm install -g newman-reporter-htmlextra"
    },
    {
      "name": "Create newman directory",
      "run": "mkdir -p newman"
    }
  ]
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
