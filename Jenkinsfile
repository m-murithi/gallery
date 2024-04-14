pipeline {
    agent any
    
    tools {nodejs "node"} // name should be similar to name used for installer in the global tool configuration.

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/m-murithi/gallery.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Ensure required software and dependencies are installed
                sh 'npm install' 
            }
        }
        
        //stage('Test') {
        //    steps {
        //         sh 'npm test' 
        //    }
        //}
        
        stage('Deploy to Render') {
            steps {
                // Deploy to Render platform
                sh 'node server &'
            }
        }
        
        stage('Slack') {
            steps {
                slackSend channel: '#marvin_ip1', message: 'test message'
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