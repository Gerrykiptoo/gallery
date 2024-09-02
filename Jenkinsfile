pipeline {
    agent any
    tools { 
        nodejs "NodeJS 22.6.0"
        gradle "Gradle 8.10"
    }
    stages {
        stage('Clone Repository') {
            steps { 
                git 'https://github.com/Gerrykiptoo/gallery'
            }
        }
        stage('Build Project') {
            steps {
                dir('project-directory') { // Change to the subdirectory containing the Gradle build files
                    sh 'gradle build'
                }
            }
        }
        stage('Run Tests') {
            steps {
                dir('project-directory') {
                    sh 'npm install mocha'
                    sh 'npm test'
                    sh 'gradle test'
                }
            }
        }
    }
}
