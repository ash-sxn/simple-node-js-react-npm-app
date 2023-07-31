pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                def modifiedUrl = 'https://3000-' + env.GITPOD_WORKSPACE_URL.substring('https://'.length())
                echo 'If you are using Gitpod use $modifiedUrl to view the website'
                input message: 'Finished using the website? (Click "Proceed" to continue)' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
