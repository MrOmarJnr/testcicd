pipeline {
    agent any
    environment {
        DEPLOY_USER = 'admin-app-user'
        DEPLOY_SERVER = '10.247.2.59'
        DEPLOY_DIR = '/var/www'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'make'
                // Archive build artifacts if needed
                archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'make test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sshagent(['your-ssh-credentials-id']) {
                    sh "scp -r . ${DEPLOY_USER}@${DEPLOY_SERVER}:${DEPLOY_DIR}"
                }
            }
        }
    }
}
