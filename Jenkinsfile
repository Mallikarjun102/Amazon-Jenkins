pipeline {
    agent any

 environment {
        MAVEN_VERSION = '3.8.6'
        MAVEN_HOME = "${env.WORKSPACE}/apache-maven-${env.MAVEN_VERSION}"
        PATH = "${env.MAVEN_HOME}/bin:${env.PATH}"
   
        
    }
    stages {
        stage('Install Maven') {
            steps {
                sh '''
                    
                    curl -O https://archive.apache.org/dist/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.tar.gz

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

    }  
}
