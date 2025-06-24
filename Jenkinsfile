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
        stage('validate') {
            steps {
                sh 'mvn validate'
            }
        }

        stage('package') {
            steps {
                 sh 'mvn package'
            }
        }

        
    }

  

}
