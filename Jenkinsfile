pipeline {
    agent any
    environment {
        // Use PATH+EXTRA to append to PATH properly
        PATH = "/usr/bin:/bin:/opt/homebrew/bin"
    }
    stages {

        stage('pull new scm') {
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
        success {
            emailext subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                     body: "Good news!\nBuild succeeded: ${env.BUILD_URL}",
                     to: 'mallikarjunp692@gmail.com'
        }
        failure {
            emailext subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                     body: "Build failed.\nCheck details: ${env.BUILD_URL}",
                     to: 'mallikarjunp692@gmail.com'
        }
        always {
            echo 'This will always run, regardless of build result.'
        }
    }


}
