pipeline {
    agent window
      tools {
        maven 'Maven 3.9.6'  // Use the same name you gave in Global Tool Config
    }
    stages {
       
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
