pipeline {
    agent any
    stages {
        stage('init') {
            steps {
                echo "Testing..."
            }
        }

        stage('Build') {
            steps {
                echo "Building..."
            }
        }

        stage('Deploy') {
            steps {
                echo "Code deployed."
            }
        }

        stage('Testing') {
            agent reg-server01
            steps {
                echo "Reg Server01"
            }
        }

    }
}