pipeline {
    agent any

    environment {
        NEWMAN_REPORT_DIR = "newman_reports"  // تحديد المجلد الذي يحتوي على التقرير
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // تحميل الكود من المستودع
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // تثبيت Newman و htmlextra reporter
                    sh 'npm install -g newman newman-reporter-htmlextra'
                }
            }
        }

        stage('Run Postman Collection') {
            steps {
                script {
                    // تشغيل Postman Collection باستخدام Newman وتوليد التقرير
                    sh """
                    newman run "Trello API _environment.postman_collection.json" \
                    --environment "Trello.postman_environment.json" \
                    --reporters cli,htmlextra \
                    --reporter-htmlextra-export ${NEWMAN_REPORT_DIR}/report.html
                    """
                }
            }
        }

        stage('Archive Test Report') {
            steps {
                // رفع التقرير كـ artifact بعد تنفيذ الاختبارات
                archiveArtifacts artifacts: "${NEWMAN_REPORT_DIR}/report.html", allowEmptyArchive: true
            }
        }

        stage('Publish HTML Report') {
            steps {
                // نشر التقرير بتنسيق HTML داخل Jenkins
                publishHTML(target: [
                    reportDir: 'newman_reports',
                    reportFiles: 'report.html',
                    reportName: 'Newman Report'
                ])
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
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

    post {
        always {
            // بعد تنفيذ الـ pipeline
            echo 'Newman Report generation and deployment process completed.'
        }
    }
}
