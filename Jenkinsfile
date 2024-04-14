pipeline {
    agent any
    
    tools {nodejs "node"} // name should be similar to name used for installer in the global tool configuration.

    stages {
        stage('Checkout') {
            steps {
                // Checkout source code from your version control system
                git 'https://github.com/m-murithi/gallery.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Ensure required software and dependencies are installed
                sh 'npm install' 
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded! Your changes have been deployed.'
        }
        failure {
            echo 'Pipeline failed! Deployment to Render was unsuccessful.'
        }
    }
}
