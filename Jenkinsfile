pipeline {
    agent any
    tools {
        nodejs "NodeJS 22.7.0"  // Ensure this NodeJS version is installed and properly configured in Jenkins
    }
    environment {
        SLACK_WEBHOOK_URL = 'your-slack-webhook-url'  // Ensure this is the actual Slack webhook URL
        RENDER_SERVICE_ID = 'your-render-service-id'  // Ensure this is the correct Render service ID
        RENDER_API_KEY = 'your-render-api-key'  // Ensure this is the correct Render API key
        EMAIL_RECEPIENT = 'your-email@example.com'  // Replace with the actual email recipient
        EMAIL_SUBJECT_SUCCESS = 'Build SUCCESS'
        EMAIL_SUBJECT_FAILURE = 'Build FAILURE'
        EMAIL_BODY = 'The Jenkins build has completed with status: ${currentBuild.currentResult}'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master', url: 'https://github.com/Gerrykiptoo/gallery'  // Ensure this URL is correct
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'  // Ensure npm is available and the command runs successfully
            }
        }
        stage('Build Project') {
            steps {
                sh 'npm run build'  // Ensure the build script is defined in package.json
            }
        }
        stage('Deploy to Render') {
            steps {
                sh '''
                curl -X POST "https://api.render.com/v1/services/${RENDER_SERVICE_ID}/deploys" \
                -H "Accept: application/json" \
                -H "Authorization: Bearer ${RENDER_API_KEY}" \
                -d ''
                '''
            }
        }
        
        stage('Slack Notification') {
            steps {
                slackSend(channel: '#your-slack-channel', color: 'good', message: "Build Successful: ${env.JOB_NAME} - ${env.BUILD_NUMBER}")
                // Ensure Slack plugin is properly configured in Jenkins and the channel exists
            }
        }
    }
    post {
        success {
            emailext(
                attachLog: true, 
                body: EMAIL_BODY, 
                subject: EMAIL_SUBJECT_SUCCESS, 
                to: EMAIL_RECEPIENT
                // Ensure email notifications are correctly configured in Jenkins
            )
        }
        failure {
            emailext(
                attachLog: true, 
                body: EMAIL_BODY, 
                subject: EMAIL_SUBJECT_FAILURE, 
                to: EMAIL_RECEPIENT
                // Ensure email notifications are correctly configured in Jenkins
            )
        }
    }
}
