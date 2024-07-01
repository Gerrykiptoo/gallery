pipeline{
    agent any
    tools {
        nodejs 'nodejs'
    }
    stages{
        stage("Clone Repository"){
            steps{
                git branch:'master', url: 'https://github.com/Gerrykiptoo/gallery.git'
            }
        }
        stage("build"){
            steps{
                sh 'npm install'
                sh 'npm run'
            }
        }
        stage("Test"){
            steps{
                sh  './jenkins/scripts/test.sh'
            }
        }
        stage("Deploy code"){
            step{
                sh './jenkins/scripts/deliver.sh' 
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                 sh './jenkins/scripts/kill.sh'
            }
        }                                
    }
}