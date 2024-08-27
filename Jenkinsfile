pipeline {
    agent any
    environment {
        DEPLOY_USER = 'admin-app-user'
        DEPLOY_SERVER = '10.247.2.59'
        DEPLOY_DIR = '/var/www'
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
                script {
                    catchError(buildResult: 'UNSTABLE', stageResult: 'FAILURE') {
                        echo 'Building...'
                        sh 'make'
                        // Archive build artifacts if needed
                        archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
                    }
                }
            }
        }
        stage('Test') {
            when {
                expression {
                    return currentBuild.result == 'SUCCESS' || currentBuild.result == 'UNSTABLE'
                }
            }
            steps {
                echo 'Testing...'
                sh 'make test'
            }
        }
        stage('Deploy') {
            when {
                expression {
                    return currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                echo 'Deploying...'
                sshagent(['your-ssh-credentials-id']) {
                    sh "scp -r . ${DEPLOY_USER}@${DEPLOY_SERVER}:${DEPLOY_DIR}"
                }
            }
        }
    }
}
