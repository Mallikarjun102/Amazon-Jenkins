pipeline {
    agent any

 environment {
        MAVEN_VERSION = '3.8.6'
        MAVEN_HOME = "${env.WORKSPACE}/apache-maven-${env.MAVEN_VERSION}"
        PATH = "${env.MAVEN_HOME}/bin:${env.PATH}"
   
        PATH = "/usr/bin:/bin:/opt/homebrew/bin:$PATH"  // Explicitly add /usr/bin and other necessary paths
    }
    stages {
        stage('Install Maven') {
            steps {
                sh '''
                    curl -O https://downloads.apache.org/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz
                    tar -xzf apache-maven-${MAVEN_VERSION}-bin.tar.gz
                '''
            }
        }
        stage('Checkout Code') {
            steps {
                // Pull the code from the GitHub repository
                git url: 'https://github.com/Mallikarjun102/Amazon-Jenkins', branch: 'main'  // Use the desired branch
            }
        }

        stage('Build') {
            steps {
                script {
                    // Running the Maven build command
                    echo "Building the project..."
                    sh 'mvn clean install'
                }
            }
        }

        stage('Send Slack Notification via curl') {
            steps {
                script {
                    def slackWebhookUrl = 'https://hooks.slack.com/services/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'
                    
                    // Determine the build status
                    def buildStatus = currentBuild.result ?: 'SUCCESS'  // Default to SUCCESS if not explicitly set

                    // Create message based on build result
                    def message = """
                    {
                        "text": "Jenkins Build Status: ${buildStatus}",
                        "attachments": [
                            {
                                "text": "Build ${buildStatus}",
                                "color": "${buildStatus == 'SUCCESS' ? 'good' : 'danger'}"
                            }
                        ]
                    }
                    """
                    
                    // Send Slack notification with build status
                    sh """
                    curl -X POST -H 'Content-type: application/json' --data '${message}' ${slackWebhookUrl}
                    """
                }
            }
        }
    }
    post {
        always {
            // This block ensures that a message is sent regardless of success or failure
            script {
                def buildStatus = currentBuild.result ?: 'SUCCESS'
                def slackWebhookUrl = 'https://hooks.slack.com/services/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'
                def message = """
                {
                    "text": "Jenkins Build Status: ${buildStatus}",
                    "attachments": [
                        {
                            "text": "Build ${buildStatus}",
                            "color": "${buildStatus == 'SUCCESS' ? 'good' : 'danger'}"
                        }
                    ]
                }
                """
                
                // Send the build status notification to Slack
                sh """
                curl -X POST -H 'Content-type: application/json' --data '${message}' ${slackWebhookUrl}
                """
            }
        }
    }
}
