pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // or your build command
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                 // or your test command
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sh 'scp -r . admin-app-user@10.247.2.59:/tmp' // or your deployment command
            }
        }
    }
}
