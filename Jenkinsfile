pipeline {
    agent any
    stages {
        stage('Initialized') {
            steps {
                echo "Initializing"
            }
        }

        stage('Deploy to CI') {
            steps {
                build job: 'oneweb-staging-deploy'
            }
        }

        stage('Testing') {
            agent { label 'reg-server01' }
            steps {
                build job: 'S-RS-01-HomePage-Listings-Details'
            }
        }

    }
}