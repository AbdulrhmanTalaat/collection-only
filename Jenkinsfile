pipeline {
    agent any

    environment {
        NEWMAN_REPORT_DIR = "newman_reports"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
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
                    // تشغيل collection باستخدام Newman وتوليد التقرير
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
                // رفع التقرير كـ artifact بعد التشغيل
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
    }

    post {
        always {
            // يمكن هنا إرسال بريد أو إجراء أي عملية أخرى بعد التنفيذ
            echo 'Postman Collection test run completed.'
        }
    }
}
