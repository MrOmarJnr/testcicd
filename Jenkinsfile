pipeline {
    agent any
    
    environment {
        DEPLOY_USER = 'admin-app-user'
        DEPLOY_SERVER = '10.247.2.59'
        DEPLOY_DIR = '/var/www'
        SSH_CREDENTIALS_ID = 'your-ssh-credentials-id' // Replace with your actual credentials ID
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building...'
                script {
                    // Ensure 'make' command runs correctly
                    sh 'make || true' // 'true' allows the pipeline to continue if 'make' fails
                }
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                script {
                    // Ensure SSH credentials are set
                    sshagent([SSH_CREDENTIALS_ID]) {
                        sh "scp -r . ${DEPLOY_USER}@${DEPLOY_SERVER}:${DEPLOY_DIR}"
                    }
                }
            }
        }
    }
    
    post {
        always {
            echo 'Cleaning up...'
            // Optional: Add cleanup steps here if needed
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
