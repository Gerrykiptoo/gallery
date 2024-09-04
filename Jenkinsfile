pipeline {
    agent any
    tools {
        nodejs "NodeJS 22.7.0"
    }
    environment {
        SLACK_WEBHOOK_URL = 'your-slack-webhook-url'
        RENDER_SERVICE_ID = 'your-render-service-id'
        RENDER_API_KEY = 'your-render-api-key'
        HEROKU_APP_NAME = 'your-heroku-app-name'
        HEROKU_API_KEY = 'your-heroku-api-key'
        EMAIL_RECEPIENT = 'your-email@example.com'
        EMAIL_SUBJECT_SUCCESS = 'Build SUCCESS'
        EMAIL_SUBJECT_FAILURE = 'Build FAILURE'
        EMAIL_BODY = 'The Jenkins build has completed with status: ${currentBuild.currentResult}'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Gerrykiptoo/gallery'
            }
        }
        stage('Install Dependencies') {
            steps {
               sh 'npm install'
            }
        }
        stage('Build Project') {
            steps {
                sh 'npm run build'
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
        stage('Deploy to Heroku') {
            steps {
                sh '''
                echo "Deploying to Heroku..."
                git push https://heroku:${HEROKU_API_KEY}@git.heroku.com/${HEROKU_APP_NAME}.git HEAD:main
                '''
            }
        }
        stage('Slack Notification') {
            steps {
                slackSend(channel: '#your-slack-channel', color: 'good', message: "Build Successful: ${env.JOB_NAME} - ${env.BUILD_NUMBER}")
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
            )
        }
        failure {
            emailext(
                attachLog: true, 
                body: EMAIL_BODY, 
                subject: EMAIL_SUBJECT_FAILURE, 
                to: EMAIL_RECEPIENT
            )
        }
    }
}
