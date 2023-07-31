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
                sh 'echo "If you are using gitpod replace 8080 with 3000 in your URL to view the site"'
                sh 'echo $GITPOD_WORKSPACE_URL'
                input message: 'Finished using the website? (Click "Proceed" to continue)' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
