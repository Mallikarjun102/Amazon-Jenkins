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
        success {
            
            emailext ( subject: "SUCCESS: ${PROJECT_NAME - Build} #${BUILD_NUMBER}  ${BUILD_STATUS!}",
                     body: "Good news!\nBuild succeeded: ${BUILD_STATUS}",
                     to: 'abctest080@gmail.com'
                      )
        }
        failure {
            emailext ( subject: "SUCCESS: ${PROJECT_NAME - Build} #${BUILD_NUMBER}  ${BUILD_STATUS!}",
                     body: "Good news!\nBuild succeeded: ${BUILD_STATUS}",
                     to: 'abctest080@gmail.com')
        }
        always {
            echo 'This will always run, regardless of build result.'
        }
    }


}
