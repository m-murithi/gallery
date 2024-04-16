pipeline {
    agent any
    
    tools {nodejs "node"} // name should be similar to name used for installer in the global tool configuration.

    environment {
        EMAIL_SUBJECT = 'Build Failed: ${env.JOB_NAME} - ${env.BUILD_NUMBER}'
        EMAIL_BODY = 'The build of ${env.JOB_NAME} - ${env.BUILD_NUMBER} has failed. Please check Jenkins for details.'
        RENDER_APP_URL = 'https://gallery-cvvb.onrender.com'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/m-murithi/gallery.git'
            }
        }

        stage('Build') {
            steps {
                // Ensure required software and dependencies are installed
                sh 'npm install' 
            }
        }
        
        stage('Test') {
            steps {
                 sh 'npm test' 
            }
        }
        
        stage('Deploy to Render') {
            environment {
                RENDER_EMAIL = credentials('render-email') 
                RENDER_PASSWORD = credentials('render-password') 
                RENDER_SERVICE_NAME = 'gallery'
            }
            steps {
                // Log in to Render using renderctl (Render CLI)
                withCredentials([string(credentialsId: 'render-email', variable: 'RENDER_EMAIL'),
                                 string(credentialsId: 'render-password', variable: 'RENDER_PASSWORD')]) {
                    sh 'renderctl login --email=${RENDER_EMAIL} --password=${RENDER_PASSWORD}'
                }

                // Deploy the application to Render using Git integration
                sh "renderctl up ${RENDER_SERVICE_NAME} --build-branch=main"
            }
        }
        
        stage('Slack') {
            steps {
                slackSend channel: '#marvin_ip1', message: 'Build ${env.BUILD_NUMBER} completed. Site: ${RENDER_APP_URL}'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded! Your changes have been deployed.'
        }
        failure {
            mail to: 'marvin.murithi@student.moringaschool.com', 
                 subject: '${EMAIL_SUBJECT}',
                 body: '${EMAIL_BODY}'
        }
    }
}