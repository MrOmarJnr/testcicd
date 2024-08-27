pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'make' // or your build command
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'make test' // or your test command
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                sh 'scp -r . admin-app-user@10.247.2.59:/var/www' // or your deployment command
            }
        }
    }
}
