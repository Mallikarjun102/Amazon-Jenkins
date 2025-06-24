pipeline {
    agent any
    environment {
        // Use PATH+EXTRA to append to PATH properly
        PATH = "/usr/bin:/bin:/opt/homebrew/bin"
    }
    stages {
        stage('pull scm') {
            steps {
                git branch: 'main', url: 'https://github.com/PraveenKuber/Amazon-Jenkins.git'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn compile'
            }
        }

} 

    post {
        success {
            echo '✅ Pipeline succeeded!'
            // Add actions like Slack/email notifications
        }

        failure {
            echo '❌ Pipeline failed!'
            // Actions for failure, like logging or alerts
        }

        unstable {
            echo '⚠️ Pipeline is unstable!'
            // Happens if a test fails but build still proceeds
        }

        aborted {
            echo '⛔ Pipeline was aborted!'
            // Actions for when a user aborts the pipeline
        }

        always {
            echo '📌 This always runs (success, failure, aborted, unstable).'
            // Clean up or archive artifacts
        }
    }

}


