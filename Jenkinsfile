pipeline {
    agent any
    environment {
        // Use PATH+EXTRA to append to PATH properly
        PATH = "/usr/bin:/bin:/opt/homebrew/bin"
    }
    stages {

        stage('pull nw scm') {
            steps {
                git branch: 'main', url: 'https://github.com/PraveenKuber/Amazon-Jenkins.git'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn compile'
            }
        }

        stage('build') {
            steps {
                 sh 'mvn clean install'
            }
        }

        
    }

    

    post {
  always {
    emailext(
      to: 'you@example.com',
      subject: "${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
      body: """
        ${env.JOB_NAME} - Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}:

        Check console output at ${env.BUILD_URL} to view the results.
      """
    )
  }
}



}
