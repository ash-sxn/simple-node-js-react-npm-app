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
                // Remove the initial 'https://' and prepend 'https://3000-' to the URL.
                script {
                    try {
                        def modifiedUrl = 'https://3000-' + env.GITPOD_WORKSPACE_URL.substring('https://'.length())
                        echo "If you are using Gitpod use this link instead ${modifiedUrl}"
                    } catch (NullPointerException e) {
                        echo "Gitpod workspace URL not available. Skipping modification of URL."
                    }
                }
                input message: 'Finished using the website? (Click "Proceed" to continue)' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
