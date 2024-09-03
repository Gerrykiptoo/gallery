pipeline {
    agent any
    tools {
        nodejs "NodeJS 22.7.0"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Gerrykiptoo/docker_wokshop_react'
            }
        }
        stage('Install Dependencies') {
            steps {
                dir('.') {  // Root directory, where your package.json is located
                    sh 'npm install'
                }
            }
        }
        stage('Build Project') {
            steps {
                dir('.') {  // Root directory, where your package.json is located
                    sh 'npm run build'
                }
            }
        }
        stage('Run Tests') {
            steps {
                dir('.') {  // Root directory, where your package.json is located
                    sh 'npm test'
                }
            }
        }
    }
}
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
                dir('.') {  // Root directory, where your package.json is located
                    sh 'npm install'
                }
            }
        }
        stage('Build Project') {
            steps {
                dir('.') {  // Root directory, where your package.json is located
                    sh 'npm run build'
                }
            }
        }
        stage('Run Tests') {
            steps {
                dir('.') {  // Root directory, where your package.json is located
                    sh 'npm test'
                }
            }
        }
    }
}
