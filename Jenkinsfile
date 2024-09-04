pipeline {
    agent any
    tools {
        nodejs "NodeJS 22.7.0"
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
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
    }
}
