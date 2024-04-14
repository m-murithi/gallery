pipeline {
    agent any
    
    tools {nodejs "node"} // name should be similar to name used for installer in the global tool configuration.

    environment {
        EMAIL_SUBJECT = "Build Failed: ${env.JOB_NAME} - ${env.BUILD_NUMBER}"
        EMAIL_BODY = "The build of ${env.JOB_NAME} - ${env.BUILD_NUMBER} has failed. Please check Jenkins for details."
    }

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
                slackSend channel: '#marvin_ip1', message: 'Build ${env.BUILD_NUMBER} completed'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded! Your changes have been deployed.'
        }
        failure {
            mail to: 'marvin.murithi@student.moringaschool.com', 
                 subject: "${EMAIL_SUBJECT}",
                 body: "${EMAIL_BODY}"
        }
    }
}